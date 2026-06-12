# Invenbin Admin Panel

The Invenbin package includes a comprehensive Filament-based admin panel for managing inventory, products, and related data through a modern web interface.

## Accessing the Admin Panel

After installation, access the admin panel at:

```
/admin
```

Login with your Laravel application credentials.

## Admin Panel Resources

### Products

**Location:** Admin → Products

**Features:**
- View all products in a data table
- Search and filter products
- Sort by any column
- Bulk actions (delete, update status)
- Create new products
- Edit existing products
- Delete products
- View product details

**Product Form Fields:**
- SKU (required, unique)
- Product Name (required)
- Short Description
- Attribute XML
- Stock Location
- Our Price (wholesale)
- Retail Price
- Weight
- Currency Code
- Unit of Measure (dropdown)
- Admin Comments
- Dimensions (Length, Height, Width)
- Dimension Unit
- List Order
- Default Image
- Inventory Count
- Reorder Point
- Product Status (dropdown)
- Product Type (dropdown)

**Product Relations:**
- Images tab - Manage product images
- Descriptors tab - Manage product feature descriptions
- Categories tab - Assign product to categories
- Usage Logs tab - View inventory adjustment history
- Bill of Materials tab - Manage BOM (if applicable)

### Categories

**Location:** Admin → Categories

**Features:**
- Hierarchical category tree view
- Create parent and child categories
- Category images
- Short and long descriptions
- Reorder categories
- Bulk actions

**Category Form Fields:**
- Category Name (required)
- Image File
- Parent Category (dropdown for hierarchy)
- Short Description
- Long Description
- BOM ID (optional)

### Product Types

**Location:** Admin → Product Types

**Features:**
- Define product classification types
- Simple CRUD interface
- Used in product creation

**Product Type Form Fields:**
- Product Type (required)

### Product Statuses

**Location:** Admin → Product Statuses

**Features:**
- Define product availability statuses
- Common statuses: Available, Out of Stock, Discontinued, Backordered
- Used in product creation and filtering

**Product Status Form Fields:**
- Status (required)

### Units of Measure

**Location:** Admin → Units of Measure

**Features:**
- Define measurement units
- Used for product quantities and dimensions
- Examples: pieces, kg, liters, meters

**Unit of Measure Form Fields:**
- Unit Name (required)
- Abbreviation (required)

### Bill of Materials

**Location:** Admin → Bill of Materials

**Features:**
- Create BOMs for complex products
- Define components and quantities
- Associate with products
- Component management

**BOM Form Fields:**
- Product (required)
- BOM Name (required)
- Components (relation manager)
  - Item Description
  - Adjustment Units

### Product Images

**Location:** Products → Edit Product → Images Tab

**Features:**
- Upload multiple images
- Set display order
- Add captions
- Set default image
- Delete images

**Image Form Fields:**
- Image File (required)
- List Order
- Caption

### Product Descriptors

**Location:** Products → Edit Product → Descriptors Tab

**Features:**
- Add feature descriptions
- Bulleted list or text format
- Reorder descriptors
- Rich text support

**Descriptor Form Fields:**
- Title (required)
- Descriptor (required)
- Is Bulleted List (boolean)
- List Order

### Product Usage Logs

**Location:** Products → Edit Product → Usage Logs Tab

**Features:**
- View complete inventory adjustment history
- Filter by date range
- Filter by adjustment type
- Filter by user
- Export logs

**Usage Log Fields (Read-only):**
- Adjustment quantity
- Adjustment type (add, remove, transfer)
- Reason
- Created date
- Updated by (user)

## Navigation Structure

The admin panel is organized into the following sections:

### Inventory Management
- Products
- Categories
- Inventory Reports (future)

### Configuration
- Product Types
- Product Statuses
- Units of Measure

### Manufacturing
- Bill of Materials
- Components

## Filtering and Search

### Global Search
Use the search bar at the top to search across all resources.

### Resource-Specific Filters
Each resource has its own filter panel:
- Products: Filter by category, status, type, stock level
- Categories: Filter by parent category
- Usage Logs: Filter by date range, adjustment type, user

### Table Sorting
Click any column header to sort. Click again to reverse sort.

## Bulk Actions

Select multiple rows using checkboxes to access bulk actions:

### Products
- Delete
- Update Status
- Update Category
- Export

### Categories
- Delete
- Reorder

### Usage Logs
- Export
- Delete (with confirmation)

## Export Features

Export data from any resource:

1. Select rows or use "Select All"
2. Click "Export" button
3. Choose format (CSV, Excel, PDF)
4. Download file

## User Permissions

The admin panel respects Laravel's authorization system:

### Super Admins
- Full access to all resources
- Can delete any record
- Can modify system configuration

### Regular Users
- Access based on assigned permissions
- May be restricted to specific resources
- Cannot delete critical records

### Custom Roles
Define custom roles in your application's policy system.

## Customization

### Custom Fields
Add custom fields to resources by modifying the Filament resource classes:

```php
// In ErpProductResource.php
public static function form(Form $form): Form
{
    return $form
        ->schema([
            // Existing fields...
            TextInput::make('custom_field')
                ->label('Custom Field')
                ->required(),
        ]);
}
```

### Custom Actions
Add custom actions to resources:

```php
public static function getActions(): array
{
    return [
        Actions\CreateAction::make(),
        Actions\Action::make('customAction')
            ->label('Custom Action')
            ->action(function () {
                // Custom logic
            }),
    ];
}
```

### Custom Filters
Add custom filters to resources:

```php
public static function getEloquentQuery(): Builder
{
    return parent::getEloquentQuery()
        ->where('site_id', auth()->user()->currentSite()->id);
}
```

## Performance Optimization

### Eager Loading
Relations are eager-loaded by default to prevent N+1 queries.

### Caching
Consider caching frequently accessed data:

```php
public static function getTable(): Table
{
    return Table::make()
        ->columns([
            // Columns...
        ])
        ->cached();
}
```

### Lazy Loading
Large datasets use lazy loading for better performance.

## Responsive Design

The admin panel is fully responsive:
- Desktop: Full feature set
- Tablet: Optimized layout
- Mobile: Simplified interface with collapsible sidebar

## Dark Mode

Toggle dark mode using the theme switcher in the user menu.

Settings are saved per user and persist across sessions.

## Notifications

The admin panel shows notifications for:
- Successful operations (green)
- Validation errors (red)
- Informational messages (blue)
- Warnings (yellow)

Notifications auto-dismiss after 5 seconds.

## Audit Trail

All changes are tracked with:
- Created timestamp
- Updated timestamp
- Updated by (user)
- Reason (for usage logs)

View complete audit history in the Usage Logs tab.

## Integration with Main Application

The admin panel integrates with your main Laravel application:
- Uses existing authentication system
- Respects user permissions
- Shares database connections
- Can access other application resources

## Troubleshooting

### Panel Not Showing
- Ensure panel is registered in AppServiceProvider
- Clear config cache: `php artisan config:clear`
- Check Filament installation

### Resources Not Appearing
- Verify resource classes are in correct namespace
- Check that resources are not hidden
- Clear route cache: `php artisan route:clear`

### Permissions Issues
- Check user roles and permissions
- Verify policy classes are registered
- Review authorization logic in resource classes

### Performance Issues
- Enable query logging to identify slow queries
- Add database indexes on frequently filtered fields
- Consider implementing caching
- Use eager loading for relations

## Future Enhancements

Planned admin panel features:
- Dashboard with analytics
- Advanced reporting
- Chart widgets
- Kanban board for task management
- Calendar view for schedules
- Mobile app companion
- Real-time notifications
- Advanced filters with saved presets
- Custom dashboard builder
