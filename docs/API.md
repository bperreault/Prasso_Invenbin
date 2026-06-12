# Invenbin API Documentation

The Invenbin package provides a comprehensive RESTful API for managing inventory, products, and related data.

## Accessing API Documentation

Interactive API documentation is available via Swagger UI:

```
GET /api/documentation
```

This provides a web interface to explore and test all API endpoints.

## API Endpoints

### Products

#### List All Products
```http
GET /api/products
```

**Query Parameters:**
- `page` - Page number (default: 1)
- `per_page` - Items per page (default: 15)
- `category_id` - Filter by category
- `status_id` - Filter by status
- `type_id` - Filter by type
- `search` - Search in name and SKU

**Response:**
```json
{
  "data": [
    {
      "id": 1,
      "sku": "PROD-001",
      "product_name": "Sample Product",
      "short_description": "A sample product",
      "our_price": 99.99,
      "retail_price": 149.99,
      "inventory_count": 100,
      "reorder_point": 10,
      "created_at": "2024-01-01T00:00:00Z",
      "updated_at": "2024-01-01T00:00:00Z"
    }
  ],
  "meta": {
    "current_page": 1,
    "per_page": 15,
    "total": 100
  }
}
```

#### Get Single Product
```http
GET /api/products/{guid}
```

**Note:** Products use GUID (Globally Unique Identifier) instead of numeric ID.

**Response:**
```json
{
  "id": 1,
  "guid": "550e8400-e29b-41d4-a716-446655440000",
  "sku": "PROD-001",
  "product_name": "Sample Product",
  "short_description": "A sample product",
  "attribute_xml": null,
  "stock_location": "Warehouse A",
  "our_price": 99.99,
  "retail_price": 149.99,
  "weight": 1.5,
  "currency_code": "USD",
  "unit_of_measure_id": 1,
  "admin_comments": null,
  "length": 10.0,
  "height": 5.0,
  "width": 3.0,
  "dimension_unit_id": 1,
  "list_order": 0,
  "rating_sum": 45,
  "total_rating_votes": 5,
  "default_image": "product-001.jpg",
  "owned_by": 1,
  "inventory_count": 100,
  "reorder_point": 10,
  "product_status_id": 1,
  "product_type_id": 1,
  "created_at": "2024-01-01T00:00:00Z",
  "updated_at": "2024-01-01T00:00:00Z",
  "updated_by": "admin",
  "images": [],
  "descriptors": [],
  "categories": [],
  "usage_logs": []
}
```

#### Create Product
```http
POST /api/products
Content-Type: application/json
```

**Request Body:**
```json
{
  "sku": "PROD-002",
  "product_name": "New Product",
  "short_description": "A new product",
  "our_price": 99.99,
  "retail_price": 149.99,
  "inventory_count": 50,
  "reorder_point": 10,
  "product_status_id": 1,
  "product_type_id": 1,
  "unit_of_measure_id": 1
}
```

**Response:** 201 Created with the created product object (includes generated GUID)

#### Update Product
```http
PUT /api/products/{guid}
Content-Type: application/json
```

**Note:** Use the product's GUID in the URL.

**Request Body:** Same as create product (all fields optional)

**Response:** 200 OK with the updated product object

#### Delete Product
```http
DELETE /api/products/{guid}
```

**Note:** Use the product's GUID in the URL.

**Response:** 204 No Content

### Categories

#### List All Categories
```http
GET /api/categories
```

**Response:**
```json
{
  "data": [
    {
      "id": 1,
      "category_name": "Electronics",
      "image_file": "electronics.jpg",
      "parent_id": null,
      "short_description": "Electronic devices",
      "long_description": "Various electronic products",
      "created_at": "2024-01-01T00:00:00Z",
      "updated_at": "2024-01-01T00:00:00Z"
    }
  ]
}
```

#### Get Single Category
```http
GET /api/categories/{id}
```

#### Create Category
```http
POST /api/categories
Content-Type: application/json
```

**Request Body:**
```json
{
  "category_name": "New Category",
  "short_description": "A new category",
  "parent_id": null
}
```

**Response:** 201 Created with the created category object

#### Update Category
```http
PUT /api/categories/{id}
Content-Type: application/json
```

**Request Body:** Same as create category (all fields optional)

**Response:** 200 OK with the updated category object

#### Delete Category
```http
DELETE /api/categories/{id}
```

**Response:** 204 No Content

### Product Types

#### List All Product Types
```http
GET /api/product-types
```

**Response:**
```json
{
  "data": [
    {
      "id": 1,
      "product_type": "Physical Good",
      "created_at": "2024-01-01T00:00:00Z",
      "updated_at": "2024-01-01T00:00:00Z"
    }
  ]
}
```

#### Get Single Product Type
```http
GET /api/product-types/{id}
```

#### Create Product Type
```http
POST /api/product-types
Content-Type: application/json
```

**Request Body:**
```json
{
  "product_type": "Physical Good"
}
```

**Response:** 201 Created with the created product type object

#### Update Product Type
```http
PUT /api/product-types/{id}
Content-Type: application/json
```

**Request Body:** Same as create product type (all fields optional)

**Response:** 200 OK with the updated product type object

#### Delete Product Type
```http
DELETE /api/product-types/{id}
```

**Response:** 204 No Content

### Product Statuses

#### List All Product Statuses
```http
GET /api/product-statuses
```

**Response:**
```json
{
  "data": [
    {
      "id": 1,
      "status": "Available",
      "created_at": "2024-01-01T00:00:00Z",
      "updated_at": "2024-01-01T00:00:00Z"
    }
  ]
}
```

#### Get Single Product Status
```http
GET /api/product-statuses/{id}
```

#### Create Product Status
```http
POST /api/product-statuses
Content-Type: application/json
```

**Request Body:**
```json
{
  "status": "Available"
}
```

**Response:** 201 Created with the created product status object

#### Update Product Status
```http
PUT /api/product-statuses/{id}
Content-Type: application/json
```

**Request Body:** Same as create product status (all fields optional)

**Response:** 200 OK with the updated product status object

#### Delete Product Status
```http
DELETE /api/product-statuses/{id}
```

**Response:** 204 No Content

### Usage Logs

Usage logs are managed independently (not nested under products).

#### List All Usage Logs
```http
GET /api/usage-logs
```

**Query Parameters:**
- `page` - Page number (default: 1)
- `per_page` - Items per page (default: 15)
- `erp_product_id` - Filter by product

**Response:**
```json
{
  "data": [
    {
      "id": 1,
      "erp_product_id": 1,
      "adjustment": -5,
      "adjustment_type": "remove",
      "reason": "Sale",
      "created_at": "2024-01-01T00:00:00Z",
      "updated_at": "2024-01-01T00:00:00Z",
      "updated_by": "admin"
    }
  ],
  "meta": {
    "current_page": 1,
    "per_page": 15,
    "total": 50
  }
}
```

#### Get Single Usage Log
```http
GET /api/usage-logs/{id}
```

**Response:**
```json
{
  "id": 1,
  "erp_product_id": 1,
  "adjustment": -5,
  "adjustment_type": "remove",
  "reason": "Sale",
  "created_at": "2024-01-01T00:00:00Z",
  "updated_at": "2024-01-01T00:00:00Z",
  "updated_by": "admin"
}
```

#### Create Usage Log
```http
POST /api/usage-logs
Content-Type: application/json
```

**Request Body:**
```json
{
  "erp_product_id": 1,
  "adjustment": -5,
  "adjustment_type": "remove",
  "reason": "Sale"
}
```

**Response:** 201 Created with the created usage log object

#### Update Usage Log
```http
PUT /api/usage-logs/{id}
Content-Type: application/json
```

**Request Body:** Same as create usage log (all fields optional)

**Response:** 200 OK with the updated usage log object

#### Delete Usage Log
```http
DELETE /api/usage-logs/{id}
```

**Response:** 204 No Content

### Inventory

#### List All Inventory
```http
GET /api/inventory
```

**Response:**
```json
{
  "data": [
    {
      "product_id": 1,
      "product_name": "Sample Product",
      "inventory_count": 100,
      "reorder_point": 10,
      "needs_reorder": false
    }
  ]
}
```

#### Get Single Inventory Item
```http
GET /api/inventory/{item}
```

**Note:** Use product GUID or ID as the item parameter.

**Response:**
```json
{
  "product_id": 1,
  "product_name": "Sample Product",
  "inventory_count": 100,
  "reorder_point": 10,
  "needs_reorder": false
}
```

#### Update Inventory Level
```http
PUT /api/inventory/{item}
Content-Type: application/json
```

**Request Body:**
```json
{
  "inventory_count": 95
}
```

**Response:** 200 OK with updated inventory count

#### Set Reorder Point
```http
PUT /api/inventory/{item}/reorder
Content-Type: application/json
```

**Request Body:**
```json
{
  "reorder_point": 20
}
```

**Response:** 200 OK with updated reorder point

### Bill of Materials (BOM)

#### List All BOMs
```http
GET /api/bom
```

**Response:**
```json
{
  "data": [
    {
      "id": 1,
      "guid": "550e8400-e29b-41d4-a716-446655440001",
      "product_id": 1,
      "bom_name": "Product Assembly",
      "date_created": "2024-01-01T00:00:00Z",
      "created_at": "2024-01-01T00:00:00Z",
      "updated_at": "2024-01-01T00:00:00Z"
    }
  ]
}
```

#### Get Single BOM
```http
GET /api/bom/{guid}
```

**Note:** BOMs use GUID instead of numeric ID.

**Response:**
```json
{
  "id": 1,
  "guid": "550e8400-e29b-41d4-a716-446655440001",
  "product_id": 1,
  "bom_name": "Product Assembly",
  "date_created": "2024-01-01T00:00:00Z",
  "created_at": "2024-01-01T00:00:00Z",
  "updated_at": "2024-01-01T00:00:00Z",
  "components": []
}
```

#### Create BOM
```http
POST /api/bom
Content-Type: application/json
```

**Request Body:**
```json
{
  "product_id": 1,
  "bom_name": "Product Assembly"
}
```

**Response:** 201 Created with the created BOM object (includes generated GUID)

#### Update BOM
```http
PUT /api/bom/{guid}
Content-Type: application/json
```

**Note:** Use the BOM's GUID in the URL.

**Request Body:** Same as create BOM (all fields optional)

**Response:** 200 OK with the updated BOM object

#### Delete BOM
```http
DELETE /api/bom/{guid}
```

**Note:** Use the BOM's GUID in the URL.

**Response:** 204 No Content

### BOM Components

Components are nested under BOMs.

#### List Components for BOM
```http
GET /api/bom/{list_id}/components
```

**Response:**
```json
{
  "data": [
    {
      "id": 1,
      "item_description": "Component A",
      "adjustment_units": 2,
      "erp_bom_id": 1,
      "created_at": "2024-01-01T00:00:00Z",
      "updated_at": "2024-01-01T00:00:00Z"
    }
  ]
}
```

#### Get Single Component
```http
GET /api/bom/{list_id}/components/{id}
```

#### Create Component
```http
POST /api/bom/{list_id}/components
Content-Type: application/json
```

**Request Body:**
```json
{
  "item_description": "Component A",
  "adjustment_units": 2
}
```

**Response:** 201 Created with the created component object

#### Update Component
```http
PUT /api/bom/{list_id}/components/{id}
Content-Type: application/json
```

**Request Body:** Same as create component (all fields optional)

**Response:** 200 OK with the updated component object

#### Delete Component
```http
DELETE /api/bom/{list_id}/components/{id}
```

**Response:** 204 No Content

### Lookups

Lookup endpoints provide reference data for dropdowns and filters.

#### Get Categories Lookup
```http
GET /api/lookups/categories
```

**Response:**
```json
{
  "data": [
    {
      "id": 1,
      "category_name": "Electronics"
    }
  ]
}
```

#### Get Units of Measure Lookup
```http
GET /api/lookups/units-of-measure
```

**Response:**
```json
{
  "data": [
    {
      "id": 1,
      "unit_name": "Piece",
      "abbreviation": "pcs"
    }
  ]
}
```

#### Get Dimension Units Lookup
```http
GET /api/lookups/dimension-units
```

**Response:**
```json
{
  "data": [
    {
      "id": 1,
      "unit_name": "Centimeter",
      "abbreviation": "cm"
    }
  ]
}
```

#### Get Statuses Lookup
```http
GET /api/lookups/statuses
```

**Response:**
```json
{
  "data": [
    {
      "id": 1,
      "status": "Available"
    }
  ]
}
```

#### Get Product Types Lookup
```http
GET /api/lookups/types
```

**Response:**
```json
{
  "data": [
    {
      "id": 1,
      "product_type": "Physical Good"
    }
  ]
}
```

## Authentication

API endpoints may require authentication depending on your configuration. If authentication is enabled:

### Using API Token
```http
Authorization: Bearer {api_token}
```

### Using Session
```http
Cookie: laravel_session={session_id}
```

## Error Responses

### 400 Bad Request
```json
{
  "error": "Validation failed",
  "messages": {
    "sku": ["The sku field is required."]
  }
}
```

### 404 Not Found
```json
{
  "error": "Resource not found"
}
```

### 422 Unprocessable Entity
```json
{
  "error": "Validation failed",
  "messages": {
    "inventory_count": ["Inventory count cannot be negative."]
  }
}
```

### 500 Internal Server Error
```json
{
  "error": "Internal server error"
}
```

## Rate Limiting

API endpoints may be rate-limited depending on your configuration. Check response headers:

```
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
```

## Pagination

List endpoints support pagination via query parameters:

- `page` - Page number (default: 1)
- `per_page` - Items per page (default: 15, max: 100)

Response includes pagination metadata:

```json
{
  "data": [],
  "meta": {
    "current_page": 1,
    "per_page": 15,
    "total": 100,
    "last_page": 7
  },
  "links": {
    "first": "https://api.example.com/api/products?page=1",
    "last": "https://api.example.com/api/products?page=7",
    "prev": null,
    "next": "https://api.example.com/api/products?page=2"
  }
}
```

## Filtering and Sorting

### Filtering
Use query parameters to filter results:

```
GET /api/products?category_id=5&status_id=1
GET /api/usage-logs?erp_product_id=1
```

### Sorting
Use `sort` and `order` parameters:

```
GET /api/products?sort=product_name&order=asc
```

### Searching
Use `search` parameter for full-text search:

```
GET /api/products?search=laptop
```

### Important Notes

- **Products and BOMs use GUIDs** instead of numeric IDs for single resource operations
- **Usage Logs** are independent resources, not nested under products
- **Components** are nested under BOMs: `/api/bom/{list_id}/components`
- **Lookups** provide simplified reference data for dropdowns and filters
- **Inventory** has a dedicated controller with separate endpoints for listing, updating, and reorder points

## Swagger Configuration

To enable Swagger documentation:

1. Install `darkaonline/l5-swagger` package
2. Add package source path to `config/l5-swagger.php`:
```php
'paths' => [
    'annotations' => [
        base_path('app'),
        base_path('packages/faxt/invenbin/src'),
    ],
]
```
3. Generate documentation:
```bash
php artisan l5-swagger:generate
```
4. Access at `/api/documentation`

## Testing with Postman

Import the following collection structure:

```
Invenbin API
├── Products
│   ├── List Products
│   ├── Get Product (by GUID)
│   ├── Create Product
│   ├── Update Product (by GUID)
│   └── Delete Product (by GUID)
├── Categories
│   ├── List Categories
│   ├── Get Category
│   ├── Create Category
│   ├── Update Category
│   └── Delete Category
├── Product Types
│   ├── List Product Types
│   ├── Get Product Type
│   ├── Create Product Type
│   ├── Update Product Type
│   └── Delete Product Type
├── Product Statuses
│   ├── List Product Statuses
│   ├── Get Product Status
│   ├── Create Product Status
│   ├── Update Product Status
│   └── Delete Product Status
├── Usage Logs
│   ├── List Usage Logs
│   ├── Get Usage Log
│   ├── Create Usage Log
│   ├── Update Usage Log
│   └── Delete Usage Log
├── Inventory
│   ├── List All Inventory
│   ├── Get Single Inventory
│   ├── Update Inventory Level
│   └── Set Reorder Point
├── Bill of Materials
│   ├── List BOMs
│   ├── Get BOM (by GUID)
│   ├── Create BOM
│   ├── Update BOM (by GUID)
│   └── Delete BOM (by GUID)
├── BOM Components
│   ├── List Components for BOM
│   ├── Get Component
│   ├── Create Component
│   ├── Update Component
│   └── Delete Component
└── Lookups
    ├── Categories Lookup
    ├── Units of Measure Lookup
    ├── Dimension Units Lookup
    ├── Statuses Lookup
    └── Types Lookup
```

## Webhooks (Future)

Planned webhook support for real-time notifications:

- `product.created` - When a product is created
- `product.updated` - When a product is updated
- `product.deleted` - When a product is deleted
- `inventory.adjusted` - When inventory is adjusted
- `reorder.reached` - When reorder point is reached

Configure webhooks via admin panel or API.
