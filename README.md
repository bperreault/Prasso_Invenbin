# Invenbin

A comprehensive inventory management system for ERP applications.

## Documentation

Full documentation is available in the [docs](./docs) folder:

- **[INSTALLATION.md](./docs/INSTALLATION.md)** - Step-by-step installation guide
- **[FEATURES.md](./docs/FEATURES.md)** - Complete feature overview
- **[SCHEMA.md](./docs/SCHEMA.md)** - Database schema and relationships
- **[API.md](./docs/API.md)** - API endpoint documentation
- **[ADMIN_PANEL.md](./docs/ADMIN_PANEL.md)** - Admin panel user guide

## Quick Start

```bash
# Add repository to composer.json
"repositories": [
    {
        "type": "path",
        "url": "packages/faxt/invenbin"
    }
]

# Install package
composer require faxt/invenbin:dev-master

# Run migrations
php artisan migrate

# Access admin panel at /admin
# Access API docs at /api/documentation
```

## Features

- Product Management (CRUD operations)
- Inventory Tracking (stock levels, reorder points)
- Usage Logging (audit trail)
- Category Management (hierarchical organization)
- Bill of Materials (component management)
- Filament Admin Panel
- RESTful API with Swagger documentation

## Technologies

- Laravel 8+
- MySQL
- Filament
- Swagger/OpenAPI

## Support

Author: Bobbi Perreault  
Email: bcp@faxt.com  


## License

MIT License

