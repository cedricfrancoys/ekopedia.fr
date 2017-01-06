# ekopedia.fr
Ekopedia recovery notes

### Server installation
**Ubuntu 16.04.1 LTS (debian-linux-gnu 4.7.2-5)**

**MySQL 5.1.73-1**

**MediaWiki 1.17.0**  
https://phabricator.wikimedia.org/diffusion/MW/browse/REL1_17/  
source : https://codeload.github.com/wikimedia/mediawiki/tar.gz/REL1_17  
https://www.mediawiki.org/wiki/Manual:LocalSettings.php/fr  

**Apache 2.4.18**  
vérifier les erreurs apache

    tail -10 /var/log/apache2/error.log


#### configuration Apache
.htaccess  

    # Enable the rewrite engine
    RewriteEngine On
    # Short url for wiki pages
    RewriteRule ^/?wiki(/.*)?$ %{DOCUMENT_ROOT}/index.php [L]

    # Redirect / to Main Page
    RewriteRule ^/*$ %{DOCUMENT_ROOT}/index.php [L]


#### configuration Mediawiki
extensions installées  
  * Interwiki  
  * ParserFunctions  
  * WikiEditor  
  * Cite  
  * Scribunto  

Localsettings  

    <?php
    # This file was automatically generated by the MediaWiki 1.27.1
    # installer. If you make manual changes, please keep track in case you
    # need to recreate them later.
    #
    # See includes/DefaultSettings.php for all configurable settings
    # and their default values, but don't forget to make changes in _this_
    # file, not there.
    #
    # Further documentation for configuration settings may be found at:
    # https://www.mediawiki.org/wiki/Manual:Configuration_settings

    # Protect against web entry
    if ( !defined( 'MEDIAWIKI' ) ) {
        exit;
    }

    ## Uncomment this to disable output compression
    # $wgDisableOutputCompression = true;

    $wgSitename = "Ekopedia";

    ## The URL base path to the directory containing the wiki;
    ## defaults for all runtime URL paths are based off of this.
    ## For more information on customizing the URLs
    ## (like /w/index.php/Page_title to /wiki/Page_title) please see:
    ## https://www.mediawiki.org/wiki/Manual:Short_URL
    $wgScriptPath = "";

    ## The protocol and server name to use in fully-qualified URLs
    $wgServer = "http://www.ekopedia.fr";

    ## https://www.mediawiki.org/wiki/Manual:Short_URL
    $wgArticlePath = "/wiki/$1";
    $wgUsePathInfo = true;

    ## The URL path to static resources (images, scripts, etc.)
    $wgResourceBasePath = $wgScriptPath;

    ## The URL path to the logo.  Make sure you change this from the default,
    ## or else you'll overwrite your logo when you upgrade!
    $wgLogo = "$wgResourceBasePath/resources/assets/wiki.png";

    ## UPO means: this is also a user preference option

    $wgEnableEmail = false;
    $wgEnableUserEmail = true; # UPO

    $wgEmergencyContact = "apache@ekopedia.resiway.org";
    $wgPasswordSender = "apache@ekopedia.resiway.org";

    $wgEnotifUserTalk = false; # UPO
    $wgEnotifWatchlist = false; # UPO
    $wgEmailAuthentication = true;

    ## Database settings
    $wgDBtype = "mysql";
    $wgDBserver = "localhost";
    $wgDBname = "ekopedia";
    $wgDBuser = "";
    $wgDBpassword = "";

    # MySQL specific settings
    $wgDBprefix = "";

    # MySQL table options to use during installation or update
    $wgDBTableOptions = "ENGINE=InnoDB, DEFAULT CHARSET=binary";

    # Experimental charset support for MySQL 5.0.
    $wgDBmysql5 = false;

    ## Shared memory settings
    $wgMainCacheType = CACHE_ACCEL;
    $wgMemCachedServers = [];

    ## To enable image uploads, make sure the 'images' directory
    ## is writable, then set this to true:
    $wgEnableUploads = true;
    $wgUseImageMagick = true;
    $wgImageMagickConvertCommand = "/usr/bin/convert";

    # InstantCommons allows wiki to use images from https://commons.wikimedia.org
    $wgUseInstantCommons = false;

    ## If you use ImageMagick (or any other shell command) on a
    ## Linux server, this will need to be set to the name of an
    ## available UTF-8 locale
    $wgShellLocale = "en_US.utf8";

    ## Set $wgCacheDirectory to a writable directory on the web server
    ## to make your wiki go slightly faster. The directory should not
    ## be publically accessible from the web.
    #$wgCacheDirectory = "$IP/cache";

    # Site language code, should be one of the list in ./languages/data/Names.php
    $wgLanguageCode = "fr";

    $wgSecretKey = "";

    # Changing this will log out all existing sessions.
    $wgAuthenticationTokenVersion = "1";

    # Site upgrade key. Must be set to a string (default provided) to turn on the
    # web installer while LocalSettings.php is in place
    $wgUpgradeKey = "";

    ## For attaching licensing metadata to pages, and displaying an
    ## appropriate copyright notice / icon. GNU Free Documentation
    ## License and Creative Commons licenses are supported so far.
    $wgRightsPage = ""; # Set to the title of a wiki page that describes your license/copyright
    $wgRightsUrl = "https://creativecommons.org/licenses/by-sa/4.0/";
    $wgRightsText = "Creative Commons Attribution-ShareAlike";
    $wgRightsIcon = "$wgResourceBasePath/resources/assets/licenses/cc-by-sa.png";

    # Path to the GNU diff3 utility. Used for conflict resolution.
    $wgDiff3 = "/usr/bin/diff3";


    # The following permissions were set based on your choice in the installer
    $wgGroupPermissions['*']['createaccount'] = false;
    $wgGroupPermissions['*']['edit'] = true;

    ## Default skin: you can change the default skin. Use the internal symbolic
    ## names, ie 'vector', 'monobook':
    $wgDefaultSkin = "vector";

    $wgUseTidy = true;
    $wgUseImageMagick = true;
    $wgImageMagickConvertCommand = "/usr/bin/convert";

    $wgShowExceptionDetails = false; 

    # Enabled skins.
    # The following skins were automatically enabled:
    wfLoadSkin( 'CologneBlue' );
    wfLoadSkin( 'Modern' );
    wfLoadSkin( 'MonoBook' );
    wfLoadSkin( 'Vector' );


    # Enabled extensions. Most of the extensions are enabled by adding
    # wfLoadExtensions('ExtensionName');
    # to LocalSettings.php. Check specific extension documentation for more details.
    # The following extensions were automatically enabled:
    wfLoadExtension( 'Interwiki' );
    wfLoadExtension( 'ParserFunctions' );
    wfLoadExtension( 'WikiEditor' );
    wfLoadExtension( 'Cite' );
    # Enables use of WikiEditor by default but still allows users to disable it in preferences
    $wgDefaultUserOptions['usebetatoolbar'] = 1;

    # Enables link and table wizards by default but still allows users to disable them in preferences
    $wgDefaultUserOptions['usebetatoolbar-cgd'] = 1;

    # Displays the Preview and Changes tabs
    $wgDefaultUserOptions['wikieditor-preview'] = 1;

    # Displays the Publish and Cancel buttons on the top right side
    $wgDefaultUserOptions['wikieditor-publish'] = 1;

    //wfLoadExtension( 'Scribunto' );
    require_once "$IP/extensions/Scribunto/Scribunto.php";
    $wgScribuntoDefaultEngine = 'luastandalone';
    $wgScribuntoEngineConf['luastandalone']['luaPath'] = '/home/cf/ekopedia/www2/extensions/Scribunto/engines/LuaStandalone/binaries/lua5_1_5_linux_64_generic/lua';
    # End of automatically generated settings.
    # Add more configuration options below.


### Images recovery


#### Archive.org
* **en.ekopedia.org**
   * mars 2015  
    http://web.archive.org/web/20150317065828/http://en.ekopedia.org/Main_Page  
    says '460 articles'

* **fr.ekopedia.org**

    * novembre 2015 : message d'accueil nouvelle installation nginx  
    * juin 2015 : dernière version disponible  
    http://web.archive.org/web/20150609051019/http://fr.ekopedia.org/Accueil  
    says '2500 articles'

* **base.ekopedia.org**

    http://web.archive.org/web/20150318133721/http://base.ekopedia.org/Main_Page  
    says '3047 media files'

#### Ranking
    http://www.rank2traffic.com/ekopedia.org 
    pic de consultation en 2012 : 210.000 request / day

#### Script
ruby script "wayback-machine-downloader"  
https://github.com/hartator/wayback-machine-downloader


    nohup wayback_machine_downloader http://fr.ekopedia.org --to 20150609051019 &
    nohup wayback_machine_downloader http://base.ekopedia.org --to 20150318133721 &

compter le nombre de fichiers écrits :  
```
find . -type f | wc -l
```
taille d'un dossier
```
du . -sh
```

### Import images

Version sans les images : un message indique que les images ont été déplacées vers 'base'

Le fichier ekobase.sql est vide
ekopediaen.sql et ekopediafr.sql ne contiennent pas les infos sur les images (table images vide)



1) récupérer les images sur archive.org  
  * fr.ekopedia.org : 6,7 MB / 328 images
  * base.ekopedia.org : 23 MB / 1694 images

2) linéariser  
 * sortir de la structure
 * prendre uniq. la résolution la plus haute

**Script PHP:**
```php
    if ($handle = @opendir('./images')) {
        while (false !== ($entry = readdir($handle))) {
            $filepath = './images/'.$entry;
            if(is_file($filepath)) {
            
                $parts = explode('-', $entry);
                
                for($i = 0, $j = count($parts); $i < $j; ++$i) {
                    if(strpos($parts[$i], 'px') === false) break;
                }
                // all parts contained 'px' string: use the last part
                if($i == $j) --$i;
                
                // remove parts about resolution
                for($k = 0; $k < $i; ++$k) unset($parts[$k]);
                
                // merge all remaining parts
                $name = implode('-', $parts);
                
                // debug
                // echo $name."\n";
                
                $destpath = './images_dest/'.$name;
                
                // if destination file already exist and is bigger, do not copy current file
                if(file_exists($destpath) && (filesize($destpath) >= filesize($filepath))) { 
                    continue;
                }       
                
                // copy / overwrite destination file
                copy($filepath, $destpath);
            }
        }
        closedir($handle);
    }
```
3) utilisation du script d'import d'images
https://www.mediawiki.org/wiki/Manual:ImportImages.php

```
find /home/cf/ekopedia/fr.ekopedia.org/images -type f -print0 | xargs -0 mv -t /home/cf/ekopedia/images_recovery
find /home/cf/ekopedia/base.ekopedia.org/images -type f -print0 | xargs -0 mv -t /home/cf/ekopedia/images_recovery

find /home/cf/websites/fr.ekopedia.org/images -type f -exec cp '{}' /home/cf/websites/images \;
find /home/cf/websites/base.ekopedia.org/images -type f -exec cp '{}' /home/cf/websites/images \;
```

--> 1977 images

```
php maintenance/importImages.php --overwrite /home/cf/ekopedia/images_recovery  
```

### Import large SQL dumps
```
mysql -u root -p

set global net_buffer_length=1000000; --Set network buffer length to a large byte number

set global max_allowed_packet=1000000000; --Set maximum allowed packet size to a large byte number

SET foreign_key_checks = 0; --Disable foreign key checking to avoid delays,errors and unwanted behaviour

source file.sql --Import your sql dump file

SET foreign_key_checks = 1; --Remember to enable foreign key checks when procedure is complete!
```


### Upgrade Ekopedia

Pour l'export, il est préférable d'avoir des liens spéciaux en anglais (Special:, File:)

    convertir 'Fichier' en 'File'  
    convertir 'Spécial' en 'Special'

Restrictions syntaxiques (nouveau moteur moins permissif)  

    convertir <References /> en <references />
