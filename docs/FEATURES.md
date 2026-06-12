# Invenbin Features

The Invenbin Inventory Management System provides comprehensive tools for managing products, inventory, and related data in an ERP environment.

## Core Features

### Product Management
- **Create, Update, Delete Products**: Full CRUD operations for product management
- **Product Details**: Track SKU, product name, descriptions, pricing, weight, dimensions
- **Product Images**: Upload and manage multiple product images with captions
- **Product Descriptors**: Add bulleted or text descriptors for product features
- **Stock Location**: Track physical location of inventory items
- **Pricing Management**: Set wholesale and retail prices with currency support

### Inventory Management
- **Stock Level Tracking**: Monitor current inventory counts for all products
- **Reorder Points**: Set automatic reorder thresholds
- **Inventory Adjustments**: Log manual inventory changes with reasons
- **Usage Logging**: Track product usage with quantity, location, and user details
- **Inventory Reports**: Generate reports on stock levels and usage patterns

### Category Management
- **Hierarchical Categories**: Organize products into nested category structures
- **Category Images**: Add images to categories for visual navigation
- **Featured Products**: Mark products as featured within categories
- **Category Descriptions**: Add short and long descriptions for categories
- **Category Ordering**: Control display order of products within categories

### Product Type Management
- **Product Classification**: Define different product types for organization
- **Type-Based Filtering**: Filter and group products by type
- **Custom Types**: Create custom product types specific to your business needs

### Product Status Management
- **Status Tracking**: Manage product availability and condition statuses
- **Custom Statuses**: Define custom status values (e.g., Available, Out of Stock, Discontinued)
- **Status History**: Track status changes over time
- **Status-Based Filtering**: Filter products by current status

### Bill of Materials (BOM)
- **BOM Creation**: Create bills of materials for complex products
- **Component Management**: Define components and quantities for each BOM
- **BOM Templates**: Save and reuse BOM templates
- **Component Adjustments**: Manage adjustment units for precise inventory control

### Unit of Measure Management
- **Multiple Units**: Define different units of measure (e.g., pieces, kg, liters)
- **Conversion Support**: Track dimension units for length, width, height
- **Standard Units**: Ensure consistent measurement across the system

### Usage Logging
- **Detailed Logs**: Record all inventory adjustments with timestamps
- **User Tracking**: Track which users made inventory changes
- **Reason Codes**: Capture reasons for inventory adjustments
- **Adjustment Types**: Support different adjustment types (add, remove, transfer)
- **Audit Trail**: Complete history of all inventory movements

### Image Management
- **Multiple Images**: Upload multiple images per product
- **Image Ordering**: Control display order of product images
- **Image Captions**: Add descriptive captions to images
- **Default Images**: Set a default image for product listings

### Product Descriptors
- **Feature Lists**: Create bulleted lists of product features
- **Text Descriptors**: Add detailed text descriptions
- **Descriptor Ordering**: Control display order of descriptors
- **Flexible Formatting**: Support for both bulleted and text formats

### API Access
- **RESTful API**: Full API access for all operations
- **Swagger Documentation**: Interactive API documentation at `/api/documentation`
- **Third-Party Integration**: Easy integration with external systems
- **Webhook Support**: (Future feature) Webhooks for real-time updates

### Admin Panel
- **Filament Integration**: Modern, responsive admin interface
- **Bulk Operations**: Perform bulk updates and deletions
- **Advanced Filtering**: Filter and search across all data
- **Export Capabilities**: Export data in various formats
- **Role-Based Access**: Control access based on user roles

## Database Schema

The system uses a comprehensive database schema with the following main tables:

- `erp_products` - Core product data
- `erp_categories` - Product categories
- `erp_product_types` - Product type definitions
- `erp_product_statuses` - Product status definitions
- `erp_units_of_measure` - Unit of measure definitions
- `erp_bill_of_materials` - BOM definitions
- `erp_components` - BOM components
- `erp_images` - Product images
- `erp_product_descriptors` - Product feature descriptions
- `erp_product_category_maps` - Product-category relationships
- `erp_product_usage_logs` - Inventory adjustment history

See [SCHEMA.md](SCHEMA.md) for detailed schema documentation and relationship diagrams.

## Use Cases

### Retail Operations
- Manage product catalogs
- Track inventory across multiple locations
- Set up reorder points for automatic restocking
- Generate usage reports for forecasting

### Manufacturing
- Create bills of materials for finished goods
- Track component inventory
- Log material usage in production
- Manage product variations and types

### Wholesale Distribution
- Set wholesale and retail pricing
- Manage product categories for customer navigation
- Track inventory across warehouses
- Generate reports for sales analysis

### E-commerce Integration
- Provide product data to online stores
- Sync inventory levels in real-time
- Manage product images and descriptions
- Track product availability status

## Future Enhancements

Planned features for future releases:
- Barcode/QR code scanning support
- Multi-warehouse management
- Advanced reporting and analytics
- Supplier management
- Purchase order integration
- Sales order tracking
- Mobile app support
