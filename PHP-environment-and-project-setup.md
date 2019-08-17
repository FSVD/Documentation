# Development environment setup

Install [Wamp Server](http://www.wampserver.com/en/) - Apache, MySQL, PHP.

- Check installation by left click on Windows taskbar Wamp icon and select <strong>Localhost</strong> from the Wamp menu.<br>
  <i>(By default Wamp installs Apache server to listen on port 80. If port 80 is already occuped by other service (e.g. IIS) change Apache port by right click on Windows taskbar Wamp icon and select > <strong>Tools</strong> > <strong>Use a port other than 80</strong>, in Port used by Apache: 80 section).</i>
- Activate <strong>Menu item: Online/Offline</strong> option by right click on Windows taskbar Wamp icon and select > <strong>wamp settings</strong> > <strong>Menu item: Online/Offline</strong>.
- If you have a previus MySQL instance running on your computer change Wamp MySQL instance port by right click on Windows taskbar Wamp icon and select > <strong>Tools</strong> > <strong>Use a port other than 3306</strong>, in Port used by MySQL: 3306 section.
- The default directory in witch you have to store your projects is <strong>C:/wamp64/www</strong>.<br>
  If you want to store your projects in another folder add a virtual host that point to your new project folder <strong>(e.g. E:/wamphost/www)</strong> by left click on Windows taskbar Wamp icon and select > <strong>Your VirtualHosts</strong> > <strong>VirtualHost Management</strong>.<br>
  <i>(When you create a virtual host a new host IP will be added to the windows host file C:\Windows\System32\drivers\etc\hosts).</i>
- Alteratively, you can change the default www folder location by left click on Windows taskbar Wamp icon and select > <strong>Apache</strong> > <strong>httpd-vhosts.conf</strong> and change the DocumentRoot path to:<br>
  DocumentRoot "{ your virtual host root }" (e.g. E:/www)<br>
  <Directory "{ your virtual host root }"> (e.g. E:/www/)<br>
  <i>(Take into account that changing default folder could make some Wamp menu option unavailable)</i>.
- Start all wamp services by left click on Windows taskbar Wamp icon and select > <strong>Start all services</strong>.
- Put server online by left click on Windows taskbar Wamp icon and select > <strong>Put Online</strong>.<br>

Install [Composer](https://getcomposer.org/).<br><br>

### Code editor: Visual Studio Code

Install Visual Studio Code [PHP intellisense](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-intellisense), [PHP CodeSniffer](https://marketplace.visualstudio.com/items?itemName=ikappas.phpcs) and [PHP CS Fixer](https://marketplace.visualstudio.com/items?itemName=junstyle.php-cs-fixer) extensions using following commands in VSCode shell.

- code --install-extension felixfbecker.php-intellisense
- code --install-extension ikappas.phpcs
- code --install-extension junstyle.php-cs-fixer

### PHP intellisense setup

#### Edit VSCode settings (File > Preferences > Settings) and add following configuration:

```
"php.suggest.basic": false
```

### PHP code sniffer (PHPCS) setup

Install phpcs linter package grobally using following command in VSCode shell.

```
composer global require squizlabs/php_codesniffer
```

PHPCS comes with coding standards rule sets which are: <strong>MySource</strong>, <strong>PEAR</strong>, <strong>PSR1</strong>, <strong>PSR12</strong>, <strong>PSR2</strong>, <strong>Squiz</strong>, <strong>Zend</strong>.<br>
You can check installed standards using following command in VSCode shell:

```
phpcs -i
```

#### Edit VSCode settings (File > Preferences > Settings) and add following configuration:

```
"phpcs.standard": "PSR2"
```

<i>You can choose anyone of the available rule sets as default coding standard.</i><br><br>

If you are a Wordpress developer and want to use Wordpress code standard install Wordpress rule set globally following next steps.

#### Create a folder named "rule-sets" in %USERPROFILE%\AppData\Roaming\Composer\vendor\squizlabs and navigate to rule-sets folder.

```
cd %USERPROFILE%\AppData\Roaming\Composer\vendor\squizlabs\rule-sets
```

#### Clone Wordpress code standard standard git ropo in rule-sets folder.

```
git clone -b master https://github.com/WordPress/WordPress-Coding-Standards.git wpcs
```

#### Add wordpress rule set path to the PHP_CodeSniffer configuration executing following command:

```
phpcs --config-set installed_paths %USERPROFILE%\AppData\Roaming\Composer\vendor\squizlabs\rele-sets\wpcs
```

#### Check installation using following command in VSCode shell:

```
phpcs -i
```

Now you can set <strong>phpcs.standard</strong> attribute in VSCode settings file to <strong>Wordpress</strong>

### PHPCS fixer setup

Install PHP CS Fixer package grobally using following command in VSCode shell.

```
composer global require friendsofphp/php-cs-fixer
```

#### Edit VSCode settings (File > Preferences > Settings) and add following configuration:

```
"php-cs-fixer.executablePath": "%USERPROFILE%\AppData\Roaming\Composer\vendor\bin\php-cs-fixer", // Edit to point to php-cs-fixer file in your local machine.
"php-cs-fixer.executablePathWindows": "%USERPROFILE%\AppData\Roaming\Composer\vendor\bin\php-cs-fixer.bat", // Edit to point to php-cs-fixer.bat file in your local machine.
"php-cs-fixer.onsave": true,
"php-cs-fixer.rules": "@PSR2",
"php-cs-fixer.config": ".php_cs;.php_cs.dist",
"php-cs-fixer.allowRisky": false,
"php-cs-fixer.pathMode": "override",
"php-cs-fixer.exclude": [
    "*/vendor/*"
  ], // Exclude vendor folder from scanning
"php-cs-fixer.autoFixByBracket": true,
"php-cs-fixer.autoFixBySemicolon": false,
"php-cs-fixer.formatHtml": false,
"php-cs-fixer.documentFormattingProvider": true
```

<br>

# Specific framework project setup

### Laravel project installation and usage:

Install [Laravel](https://laravel.com/) framework grobally using following command in VSCode shell.

```
composer global require laravel/installer
```

Edit Windows \$PATH environment variable to include laravel executable.

```
%USERPROFILE%\AppData\Roaming\Composer\vendor\bin
```

Navigate to your virtual host folder (default <strong>C:/wamp64/www</strong>) and create a new Laravel project using following command in VSCode shell.

```
laravel new project-name
```

Install phpcs linter package for your project using following command in VSCode shell.

```
composer require --dev squizlabs/php_codesniffer
```

<i>If you want to use a specific code standard or override specific rules or add custom rules for current project different from default code standard you can use annotated rules.<br>
Create <strong>phpcs.xml</strong> file in your root directory and set your custom code standard/rules.</i>

Go to [http://localhost/project-name/public](http://localhost/project-name/public).

### RawPHP project installation and usage:

Navigate to your virtual host folder (default <strong>C:/wamp64/www</strong>) and install [RawPHP](https://github.com/rawphp-framework/rawphp) framework using following command in VSCode shell.

```
composer create-project --prefer-dist partner/rawphp project-name
```

Go to [http://localhost/project-name/public/](http://localhost/project-name/public).

<br>

# Debug configuration setup

Install Visual Studio Code [PHP debug](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug) extension using following command in VSCode shell.

- code --install-extension felixfbecker.php-debug

Wamp server comes with <strong>xDebug</strong> extension in order to debug your PHP projects.

- Activate xDebug by left click on Windows taskbar Wamp icon and select > <strong>PHP</strong> > <strong>PHP settings</strong> > <strong>xdebug.remote_enable</strong>.
- Edit <strong>php.ini</strong> by left click on Windows taskbar Wamp icon and select > <strong>PHP</strong> > <strong>php.ini</strong> and add following line in the <strong>[xdebug]</strong> section.

```
xdebug.remote_autostart = 1
```

Use following configuration in <strong>launch.json</strong> file to debug project.

```
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Listen for XDebug",
      "type": "php",
      "request": "launch",
      "port": 9000,
      "ignore": ["**/vendor/**/*.php"]
    },
    {
      "name": "Launch currently open script",
      "type": "php",
      "request": "launch",
      "program": "${file}",
      "cwd": "${fileDirname}",
      "port": 9000
    }
  ]
}
```

<i>If you configured XDebug and VSCode like recommended above, everytime you make a request with a browser to your webserver XDebug will connect and stop on breakpoints, exceptions etc. in VSCode debug panel.</i>
