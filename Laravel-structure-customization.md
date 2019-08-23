### Change project name and set the application namespace

In command line run:

```
php artisan app:name your-app-name
```

### Rename project app folder

- Rename <strong>app</strong> folder to your favourite name (e.g. src, lib etc).
- Edit <strong>composer.json</strong> file PSR-4 object as follow.

```
"autoload": {
    "psr-4": {
        "App\\": "your_new_directory/"
    }
  },
```

- Then in command line run:

```
composer dump-autoload
```

### Adding Domain Driven Design (DDD) support

Install laravel-modules package using following command in VSCode shell.

```
composer require nwidart/laravel-modules
```

Publish configuration file using following command in VSCode shell.

```
php artisan vendor:publish --provider="Nwidart\Modules\LaravelModulesServiceProvider"
```

Edit <strong>composer.json</strong> file PSR-4 object as follow.

```
"autoload": {
    "psr-4": {
        "App\\": "your_new_directory/",
        "Modules\\": "Modules/"
    }
  },
```

Reload classes using following command in VSCode shell.

```
composer dump-autoload
```

Create your own module/domain using following command in VSCode shell.

```
php artisan module:make your-module-name
```

<i>You'll find full documentation on https://nwidart.com/laravel-modules/.</i>
