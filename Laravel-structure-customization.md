# Change project name and set the application namespace

In command line run:

```
php artisan app:name your-app-name
```

<br>

# Rename project app folder

Rename <strong>app</strong> folder to your favourite name (e.g. src).<br>
Edit <strong>composer.json</strong> file PSR-4 object as follow.

```
"autoload": {
    "psr-4": {
        "App\\": "src/"
    }
  },
```

Create a new <strong>Application.php</strong> wherever you want (e.g. app folder), extends default Laravel application class adding a protected <strong>\$appPath</strong> attribute with <strong>\_\_DIR\_\_</strong> value.

```
<?php

namespace App;

use Illuminate\Foundation\Application as IlluminateApplication;

class Application extends IlluminateApplication
{
    protected $appPath = __DIR__;
}
```

In the <strong>bootstrap/app.php</strong> file edit app instance creation pointing to new <strong>Application</strong> class.

```
$app = new App\Application(
    $_ENV['APP_BASE_PATH'] ?? dirname(__DIR__)
);
```

Execute following command in VSCode shell.

```
composer dump-autoload
```

<br>

# Add Domain Driven Design (DDD) support and configuration

Install laravel-modules package using following command in VSCode shell.

```
composer require nwidart/laravel-modules
```

Publish configuration file using following command in VSCode shell.

```
php artisan vendor:publish --provider="Nwidart\Modules\LaravelModulesServiceProvider"
```

Edit <strong>modules.php</strong> config file in <strong>src\config</strong> folder.

```
'namespace' => 'Domains',

// ... rest of the code

'paths' => [
    'modules' => base_path('src/Domains'),

    // ... rest of the code

],

```

Edit <strong>composer.json</strong> file PSR-4 object as follow.

```
"autoload": {
    "psr-4": {
        "App\\": "src/",
        "Domains\\": "src/Domains"
    }
  },
```

Execute following command in VSCode shell.

```
composer dump-autoload
```

Create your own module/domain using following command in VSCode shell.

```
php artisan module:make your-module-name
```

<i>You'll find full documentation on https://nwidart.com/laravel-modules/.</i>
