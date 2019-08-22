### Change project name and set the application namespace

In command line run:

```
php artisan app:name your-app-name
```

### Rename project app folder

- Rename <strong>app</strong> folder to your favourite name (e.g. src, lib etc).
- Edit <strong>composer.json</strong> file PSR-4 attribute as follow.

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
