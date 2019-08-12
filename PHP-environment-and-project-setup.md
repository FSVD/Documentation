# Development environment setup

Install [Composer](https://getcomposer.org/).<br>
Install and configure [Wamp Server](http://www.wampserver.com/en/) - Apache, MySQL, PHP.

- Launch Wamp Server installer.
- Change default browser to Google Chrome.
- Leave default editor to notepad or change to your favourite.
- When installation finish launch Wamp Server clicking on icon in Windows start menu.
- Check installation by left click on Windows taskbar Wamp icon and select <strong>Localhost</strong> from the Wamp menu.<br>
  <i>(By default Wamp installs Apache server to listen on port 80. If port 80 is already occuped by other service (e.g. IIS) change Apache port by right click on Windows taskbar Wamp icon and select > <strong>Tools</strong> > <strong>Use a port other than 80</strong> in Port used by Apache: 80 section).</i>
- Activate Menu item: Online/Offline option by right click on Windows taskbar Wamp icon and select > <strong>wamp settings</strong> > <strong>Menu item: Online/Offline</strong>.
- If you have a previus MySQL instance running on your computer change Wamp MySQL instance port by right click on Windows taskbar Wamp icon and select > <strong>Tools</strong> > <strong>Use a port other than 3306</strong> in Port used by MySQL: 3306 section
- The default directory in witch you have to store your projects is <strong>C:/wamp64/www</strong>.<br>
  If you want to store your projects in another folder add a virtual host that point to your new project folder <strong>(e.g. E:/wamphost/www)</strong> by left click on Windows taskbar Wamp icon and select > <strong>Your VirtualHosts</strong> > <strong>VirtualHost Management</strong><br>
  <i>(When you create avirtual host a new host IP will be added to windows host file C:\Windows\System32\drivers\etc\hosts)</i>
- Alteratively, you can change the default www folder location by left click on Windows taskbar Wamp icon and select > <strong>Apache</strong> > <strong>httpd-vhosts.conf</strong> and change the DocumentRoot path to:<br>
  DocumentRoot "{ your virtual host root }" (e.g. E:/www)<br>
  <Directory "{ your virtual host root }"> (e.g. E:/www/)<br>
  <i>(Take into account that changing default folder could make some Wamp menu option unavailable)</i>.
- Start all wamp services by left click on Windows taskbar Wamp icon and select > <strong>Start all services</strong>.
- Put server online by left click on Windows taskbar Wamp icon and select > <strong>Put Online</strong>.<br><br>

### Code editor: Visual Studio Code

Install Visual Studio [PHP intellisense](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-intellisense), [PHP CodeSniffer](https://marketplace.visualstudio.com/items?itemName=ikappas.phpcs) and [PHP CS Fixer](https://marketplace.visualstudio.com/items?itemName=junstyle.php-cs-fixer) extensions using following commands in VSCode shell.

- code --install-extension felixfbecker.php-intellisense
- code --install-extension ikappas.phpcs
- code --install-extension junstyle.php-cs-fixer

### PHP intellisense setup

#### Edit VSCode settings (File > Preferences > Settings) and add following configuration:

```
"php.suggest.basic": false
```

### PHP code sniffer (PHPCS) setup

Install phpcs linter package grobally using following command in VSCode shell:

```
composer global require squizlabs/php_codesniffer
```

PHPCS comes with coding standards rule sets which are: <strong>MySource</strong>, <strong>PEAR</strong>, <strong>PSR1</strong>, <strong>PSR12</strong>, <strong>PSR2</strong>, <strong>Squiz</strong>, <strong>Zend</strong>.<br>
You can check installed standards using following command in VSCode shell:

```
phpcs -i
```

If you prefer you can add Wordpress rule-set installing it globally using following commands in VSCode shell:

Create a folder named "rule-sets" in %USERPROFILE%\AppData\Roaming\Composer\vendor\squizlabs.

```
cd %USERPROFILE%\AppData\Roaming\Composer\vendor\squizlabs\rule-sets
```

Clone Wordpress code standard standard git ropo in rule-sets folder.

```
git clone -b master https://github.com/WordPress/WordPress-Coding-Standards.git wpcs
```

Add wordpress rule set path to the PHP_CodeSniffer configuration executing following command:

```
phpcs --config-set installed_paths %USERPROFILE%\AppData\Roaming\Composer\vendor\squizlabs\rele-sets\wpcs
```

Check installation using following command in VSCode shell:

```
phpcs -i
```

#### Edit VSCode settings (File > Preferences > Settings) and add following configuration:

```
"phpcs.standard": "PSR2"
```

You can choose anyone of the available rule sets as default coding standard.

### PHPCS fixer setup

Install PHP CS Fixer package grobally using following command in VSCode shell:

```
composer global require friendsofphp/php-cs-fixer
```

#### Edit VSCode settings (File > Preferences > Settings) and add following configuration:

```
"php-cs-fixer.executablePath": "php-cs-fixer",
"php-cs-fixer.executablePathWindows": "php-cs-fixer.bat",
"php-cs-fixer.onsave": true,
"php-cs-fixer.rules": "@PSR2",
"php-cs-fixer.config": ".php_cs;.php_cs.dist",
"php-cs-fixer.allowRisky": false,
"php-cs-fixer.pathMode": "override",
"php-cs-fixer.exclude": [],
"php-cs-fixer.autoFixByBracket": true,
"php-cs-fixer.autoFixBySemicolon": false,
"php-cs-fixer.formatHtml": false,
"php-cs-fixer.documentFormattingProvider": true
```

# Project setup

...
