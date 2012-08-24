# cwsoft-addon-file-editor module for CMS WebsiteBaker 2.8.x

The `cwsoft-addon-file-editor` (consecutively abbreviated `AFE`) enables you to *view*, *edit*, *delete*, *create*, *upload*, *unzip* or *backup* files of installed Add-ons such as *modules*, *templates* or *languages* from the [WebsiteBaker CMS](http://www.websitebaker2.org) backend. `AFE` allows you to create installation packages of installed Add-ons, ready for installation in WebsiteBaker - handy for distribution or backup purposes.

The optional FTP layer implemented in `AFE`, allows you to modify Add-on files normally owned by the *ftp-user*. This might be usefull if your website is hosted on a shared hosting provider using different pemissions for PHP and FTP groups. Another optional feature is the support for the 3rd party online photo editing service [Pixlr](http://pixlr.com), which allows you to modifiy images of Add-ons in a Photoshop&trade; like environment from the WebsiteBaker backend.

## Download
The released stable `cwsoft-addon-file-editor` installation packages for the WebsiteBaker CMS can be found in the [GitHub download area](https://github.com/cwsoft/wb-addon-file-editor/downloads). It is recommended to install/update to the latest available version listed. Older versions are provided for compatibility reasons with older WebsiteBaker versions and may contain bugs or security issues. The development history of `AFE` can be tracked via [GitHub](https://github.com/cwsoft/wb-addon-file-editor).

## License
`cwsoft-addon-file-editor` is licensed under the [GNU General Public License (GPL) v3.0](http://www.gnu.org/licenses/gpl-3.0.html).

## Requirements

The minimum requirements to get `AFE` running on your WebsiteBaker installation are as follows:

- WebsiteBaker ***v2.8.1*** or higher (recommeded last stable 2.8.x version)
- PHP ***5.2.2*** or higher (recommended last stable PHP 5.3.x version)
- Optional: browser with [Flash&trade; plugin](http://get.adobe.com/de/flashplayer/) to use the [Pixlr](http://pixlr.com) image online service

## Installation

1. download [cwsoft-addon-file-editor v2.5.0](https://github.com/downloads/cwsoft/wb-addon-file-editor/cwsoft-addon-file-editor-v2.5.0.zip) WebsiteBaker installation package
2. log into your WebsiteBaker backend and go to the `Add-ons/Modules` section
3. install the downloaded zip archive via the WebsiteBaker installer
4. go to the `Admin-Tools` section and click the `AFE` tool link

## Usage

### Overview Panel
Once `AFE` is installed, visit the ***Admin-Tools*** section of your WebsiteBaker backend and click on the `AFE` admin tool link. This brings you to the `AFE` overview panel.

![](https://github.com/cwsoft/wb-addon-file-editor/raw/master/.screenshots/afe-overview-panel.png) 

The `AFE` overview panel lists all installed Add-ons of your WebsiteBaker installation. The Add-ons are grouped into the sections ***Modules***, ***Templates*** and ***Languages***. You can expand/collaps groups to show only the Add-ons you are interested in, providing you have JavaScript enabled in your browser. The toggle status of the groups is stored in a Cookie and will be remembered during the lifetime of this Cookie.

When a group is expanded, all installed Add-ons of this group are shown in a list view. A *download icon* is shown at the right side of each Add-on entry. A click on this icon creates an installation package of this Add-on on the fly. Use this option to create a ***backup*** of an Add-on ***BEFORE*** you modify it, so you can revert back to the original version in case you mess up something.

To browse the files and folders of a specific Add-on in the `AFE` file manager, click on the Add-on name you are interested in and you will be redirected to the `AFE` file manager.

### File Manager
The file manager shows the files and folders of the selected Add-on. 

![](https://github.com/cwsoft/wb-addon-file-editor/raw/master/.screenshots/afe-file-manager.png) 

Per default, only files with ***recognized*** file extensions are displayed (text, images, archives). You can add/remove file extension via `AFE` configuration file ***code/config.php***. Details about `AFEs` configuration settings are shown in section [AFE Configuration Settings](https://github.com/cwsoft/wb-addon-file-editor#configuration-settings).

To *edit* a text file, or to *view* an image in the browser, just click on the file name. To *rename* or *delete* files, click one the ***action icons*** on the right site of the file manager. You can *create* new files/folders or *upload* a file via the **action links** at the top of the file manager. The *[Reload]* option forces to read in all files and folders again. Use this option if you have installed a new Addon via the WebsiteBaker backend and it doesn�t show up in `AFE`.

#### Online Image Editing
If you click on the *edit* icon at the right of an image file, the image will be transferred to the online image editor service of [Pixlr](http://pixlr.com), allowing you to edit the image in a Photoshop&trade; like environment. Using the Pixlr *save* dialogue will save the modified image as ***image_name.pixlr.jpg*** in the actual Add-on folder. The original image remains untouched on your server. If you are happy with the image changes made, delete the original image and rename the modified image. Keep in mind that your image is uploaded to the pixlr.com server. So please read the Pixlr [FAQ](http://pixlr.com/faq/) and [Terms & Service](http://pixlr.com/terms_of_service/) ***before*** using this service. You can disable this service via the AFE configuration file ***code/config.php***.

Note: Your browser requires a [Flash&trade; plugin](http://get.adobe.com/de/flashplayer/) in order to use the online image service from [Pixlr](http://pixlr.com).

#### Unzip Archive Files
Clicking the *unzip* icon shown in the action icons group for *.zip files allows you to unzip the archive to the actual folder on your server. This allows you to create nested folder structures and/or multiple files from an existing *.zip archive with ease. The *.zip folder structure is taken over. All files contained in the target exraction folder older than the corresponding file in the archive will be replaced without further notice. 

## Configuration Settings
You can modify the default settings of `AFE` via the configuration file ***code/config.php*** located in the `AFE` module folder.

You can add/remove file exentison to the recognized file types for *text*, *image*, and *archives*. The default settings are as follows:
	
	$text_extensions = array('txt', 'htm', 'html', 'htt', 'tmpl', 'tpl', 
		'xml', 'css', 'js', 'php', 'php3', 'php4', 'php5', 'jquery', 'preset'
	);
	$image_extensions = array('bmp', 'gif', 'jpg', 'jpeg', 'png');
	$archive_extensions = array('zip', 'rar', 'tar', 'gz');

Files with extensions not listed above are *hidden* in the `AFE` file manager by default. To change this behaviour, set ***$show_all_files = true;***. 

You can remove Add-ons from the `AFE` file manager if you want. To remove `AFE` and the English language file from the `AFE` file manager, set ***$hidden_addons = array('cwsoft-addon-file-editor', 'en');*** (all lower case).

Per default, the allowed file size for uploads is limited to 2 MB (***$max_upload_size = 2***). Pixlr support (***$pixlr_support = true***) and unzip archive support (***$unzip_archive_support = true***) are enabled per default.

### FTP Configuration Settings
`AFE` implements an optional FTP layer, wich is disabled by default. You can activate this feature if required. The `AFE` file manager detects and highlights files which can't be modified by PHP in a red color. If you see Add-ons or Add-on files highlighted in red, enable the FTP layer to modify these files via FTP. The FTP layer can be configured by visiting the URL: *http://yourdomain.com/modules/cwsoft-addon-file-editor/code/ftp_assistant.php*.

Update *yourdomain.com* to fit to your domain. The URL to the FTP assistant can only be called by users/groups with permission to the WebsiteBaker Admin tools section. The FTP assistant allows you to test the FTP connection to your server, once the required FTP login information where provided. The FTP login information are stored in the `AFE` database and will be removed when you uninstall `AFE`.

## Known Issues
You can track the status of known issues or report new issues found in `AFE` via GitHubs [issue tracking service](https://github.com/cwsoft/wb-addon-file-editor/issues). If you run into any issues with `AFE`, please visit this page first and check if this issue is already known.

***Note:*** 
The 3rd party package [editarea](http://www.cdolivet.com/editarea/) distributed with WebsiteBaker (/include/editarea) has some bugs when used in Internet Explorer 8/9. Editarea is used by `AFE` and the WebsiteBaker `code` module to highlight and modify code. If you have issues to view/edit Add-on files in `AFE`, please visit the editarea [browser compatibility list](http://www.cdolivet.com/editarea/editarea/docs/compatibility.html) and check if your browser is supported by editarea. If your browser is not supported, please use a supported browser (e.g. Firefox) if you want to have syntax highlighting in WebsiteBaker working - sorry for that.

## Questions
If you have questions or issues with `AFE`, please visit the [English](http://www.websitebaker2.org/forum/index.php/topic,12122.0.html) or [German](http://www.websitebaker2.org/forum/index.php/topic,12404.0.html) WebsiteBaker forum support threads and ask for feedback.

***Always provide the following information with your support request:***

 - detailed error description (what happens, what have you tried ...)
 - the `AFE` version (go to WebsiteBaker section Add-ons / Info / AFE)
 - your PHP version (use phpinfo(); or ask your provider if in doubt)
 - WebsiteBaker version, Service Pack number and build number of your version
 - name of the WebsiteBaker backend theme used (e.g. wb_theme, argos_theme ...)
 - information about changes you made to WebsiteBaker (if any)

## Credits
Credits goes to the following WebsiteBaker forum users for translating the `AFE` language files into the following languages.

- **Dutch (NL.php):** forum members [Luckyluck](http://www.websitebaker2.org/forum/index.php?action=profile;u=6090), [pcwacht](http://www.websitebaker2.org/forum/index.php?action=profile;u=424)
- **Norwegian (NO.php):** forum member [oeh](http://www.websitebaker2.org/forum/index.php?action=profile;u=752)
- **French (FR.php):** forum member [quinto](http://www.websitebaker2.org/forum/index.php?action=profile;u=526)
