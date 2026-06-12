# Invenbin Installation Guide

This guide will help you install and configure the Invenbin inventory management package in your Laravel application.

## Prerequisites

- PHP >= 7.4
- Laravel >= 8.0
- MySQL database
- Composer package manager

## Installation Steps

### Step 1: Add Repository to Composer

This package is not hosted on Packagist - add the repository to your project's `composer.json` file.

Open your project's `composer.json` file and add the location under the `repositories` section:

```json
"repositories": [
    {
        "type": "path",
        "url": "packages/faxt/invenbin"
    }
]
```

### Step 2: Require the Package

Run the following command to require the package:

```bash
composer require faxt/invenbin:dev-master
```

If you want to install a specific version, replace `dev-master` with the desired version.

### Step 3: Register the Admin Panel

The admin panel needs registering in your app service provider before you can use it.

Open `app/Providers/AppServiceProvider.php` and add the following:

```php
use Faxt\Invenbin\Support\Facades\InvenbinPanel;

class AppServiceProvider extends ServiceProvider
{
    public function register(): void
    {
        InvenbinPanel::register();
    }
}
```

### Step 4: Publish Configuration (Optional)

If your package includes configuration files, publish them using the following command:

```bash
php artisan vendor:publish --provider="Faxt\Invenbin\InvenbinServiceProvider" --tag="config"
```

### Step 5: Configure Swagger Paths (Optional)

If you want to use Swagger for API documentation, you need to add your package's source path to the Swagger configuration.

Open `config/l5-swagger.php` and find the `paths` section. Add the path to your package's source directory:

```php
'paths' => [
    'annotations' => [
        base_path('app'),
        base_path('packages/faxt/invenbin/src'),
    ],
    'docs' => storage_path('api-docs'),
    'views' => base_path('resources/views/vendor/l5-swagger'),
],
```

**Note:** The `@OA\Info()` annotation should be added by the main application using the package.

### Step 6: Run Migrations

Run the migrations to create the database tables:

```bash
php artisan migrate
```

This will create all necessary tables for the inventory management system.

## Verification

To verify the installation:

1. Visit `/api/documentation` to view the API documentation (if Swagger is configured)
2. Check that the Filament admin panel is accessible
3. Verify that the database tables were created successfully

## Video Tutorial

A video installation tutorial is available at: [https://youtu.be/Q1346GyQjzI](https://youtu.be/Q1346GyQjzI)

## Troubleshooting

### Package not found

If you encounter a "package not found" error, ensure:
- The repository path in `composer.json` is correct
- You've run `composer dump-autoload`
- The package directory exists at the specified path

### Migration errors

If migrations fail:
- Ensure your database connection is configured in `.env`
- Check that you have the necessary database permissions
- Verify that the migrations haven't already been run

### Admin panel not showing

If the Filament admin panel doesn't appear:
- Ensure you've registered the panel in `AppServiceProvider`
- Clear your config cache: `php artisan config:clear`
- Check that Filament is properly installed in your application

## Support

For additional support or questions:
- Author: Bobbi Perreault
- Email: bcp@faxt.com
