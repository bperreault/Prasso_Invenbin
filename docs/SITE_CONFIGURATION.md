# Invenbin.com Site Configuration

This document explains how to configure invenbin.com in the database to provide admin access to all required packages.

## Overview

Invenbin.com (site_id: 6) requires the following packages to be configured in the `site_packages` and `site_package_subscriptions` tables:

- **Messaging** - SMS and email messaging capabilities
- **Church** - Church management features (members, volunteers, events)
- **Project Management** - Project tracking and management
- **Bedrock HTML Editor** - AI-powered HTML editing with AWS Bedrock

## Current State

- Invenbin.com exists in the `sites` table (id: 6)
- NO package subscriptions currently exist in `site_package_subscriptions`
- Bedrock HTML Editor package is missing from `site_packages` table

## Available Packages

The following packages exist in `site_packages` table:

| ID | Name | Slug | Status |
|----|------|------|--------|
| 1 | Messaging | messaging | Active |
| 2 | Church | church | Active |
| 3 | Project Management | project-management | Active |
| 4 | Inventory Management | invenbin | Active |
| 5 | Advanced Analytics | advanced-analytics | Active |
| 6 | Basic Site | basic-site | Active |

**Missing**: Bedrock HTML Editor package

## Configuration Steps

### Step 1: Create Bedrock HTML Editor Package

```sql
INSERT INTO site_packages (name, slug, description, is_active, created_at, updated_at)
VALUES ('Bedrock HTML Editor', 'bedrock-html-editor', 'AI-powered HTML editing with AWS Bedrock', true, NOW(), NOW());
```

After running this, note the new package_id (typically 7).

### Step 2: Subscribe Invenbin.com to Required Packages

```sql
-- Subscribe to Messaging (package_id: 1)
INSERT INTO site_package_subscriptions (site_id, package_id, subscribed_at, is_active, created_at, updated_at)
VALUES (6, 1, NOW(), true, NOW(), NOW());

-- Subscribe to Church (package_id: 2)
INSERT INTO site_package_subscriptions (site_id, package_id, subscribed_at, is_active, created_at, updated_at)
VALUES (6, 2, NOW(), true, NOW(), NOW());

-- Subscribe to Project Management (package_id: 3)
INSERT INTO site_package_subscriptions (site_id, package_id, subscribed_at, is_active, created_at, updated_at)
VALUES (6, 3, NOW(), true, NOW(), NOW());

-- Subscribe to Bedrock HTML Editor (use the ID from Step 1)
INSERT INTO site_package_subscriptions (site_id, package_id, subscribed_at, is_active, created_at, updated_at)
VALUES (6, 7, NOW(), true, NOW(), NOW());
```

### Step 3: Verify Configuration

```sql
-- Check invenbin.com subscriptions
SELECT sp.name, sp.slug, sps.subscribed_at, sps.is_active
FROM site_package_subscriptions sps
JOIN site_packages sp ON sps.package_id = sp.id
WHERE sps.site_id = 6;
```

Expected output should show 4 packages: messaging, church, project-management, and bedrock-html-editor.

## Alternative: Admin UI Configuration

You can also configure packages via the admin interface:

1. Navigate to `/admin/site-packages`
2. Click "Create Package" to add Bedrock HTML Editor
3. Select "Invenbin" from the site dropdown
4. Click "Subscribe" for each required package:
   - Messaging
   - Church
   - Project Management
   - Bedrock HTML Editor

## Additional Configuration Requirements

### Team Roles

Ensure users on invenbin.com have appropriate roles to access admin features:

- **instructor** or **site-admin** role on teams
- These roles are equivalent and provide full admin access
- Super admins have access to all sites and packages

### Site-Level Filtering

The packages implement site-level filtering:

- **Messaging**: Users only see messages from their own teams
- **Church**: Members filtered by site_id
- **Project Management**: Projects filtered by site
- **Bedrock HTML Editor**: Modifications filtered by site_id

### Site Admin Menu

The Site Admin Menu system automatically shows relevant menu items based on package subscriptions. After subscribing to packages:

1. Run the seeder: `php artisan db:seed --class=SiteAdminMenuSeeder`
2. Access `/admin` → Settings → Admin Menu
3. Customize menu items as needed

## Package-Specific Configuration

### Messaging Package

- Requires MsgTeamSetting configuration
- Set verification_status to 'verified' for full access
- Configure help_contact_email for support
- Twilio credentials in .env (TWILIO_ACCOUNT_SID, TWILIO_AUTH_TOKEN, TWILIO_PHONE_NUMBER)

### Church Package

- Set `uses_membership = true` in sites table to enable member records
- Configure volunteer positions in admin
- Members filtered by site_id in chm_members table

### Project Management Package

- Projects associated with site_id
- Team-based access control
- Uses existing team structure

### Bedrock HTML Editor Package

- Requires AWS Bedrock configuration
- Configure in config/bedrock-html-editor.php
- S3 storage for HTML modifications
- Authorization uses isInstructor() method

## Verification

After configuration, verify:

1. **Package Subscriptions**: Check `site_package_subscriptions` table
2. **Admin Access**: Log in as instructor/site-admin and verify admin menu items
3. **Package Resources**: Verify Filament resources are visible in admin panel
4. **Site Filtering**: Confirm data is filtered by site_id

## Troubleshooting

### Menu Items Not Showing

- Run `php artisan db:seed --class=SiteAdminMenuSeeder`
- Check user has instructor or site-admin role
- Verify package subscriptions are active

### Package Resources Not Visible

- Check `site_package_subscriptions.is_active = true`
- Verify package is active in `site_packages.is_active = true`
- Ensure user has appropriate team role

### Site-Level Filtering Not Working

- Verify site_id is set on relevant records
- Check team relationships are correct
- Confirm user is on correct team for the site

## Database Schema

### site_packages Table

```sql
CREATE TABLE site_packages (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    slug VARCHAR(255) UNIQUE NOT NULL,
    description TEXT NULL,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);
```

### site_package_subscriptions Table

```sql
CREATE TABLE site_package_subscriptions (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    site_id BIGINT UNSIGNED NOT NULL,
    package_id BIGINT UNSIGNED NOT NULL,
    subscribed_at TIMESTAMP NOT NULL,
    expires_at TIMESTAMP NULL,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP,
    updated_at TIMESTAMP,
    UNIQUE KEY site_package_unique (site_id, package_id),
    FOREIGN KEY (site_id) REFERENCES sites(id) ON DELETE CASCADE,
    FOREIGN KEY (package_id) REFERENCES site_packages(id) ON DELETE CASCADE
);
```

**Note**: The unique constraint on (site_id, package_id) prevents duplicate subscriptions. If you need to re-subscribe a site to a package, update the existing record instead of inserting a new one.

## Related Documentation

- [Site Admin Menu Implementation](../../../../../docs/SITE_ADMIN_MENU_IMPLEMENTATION.md)
- [Site-Level Message Filtering](../../../../../docs/SITE_LEVEL_MESSAGE_FILTERING.md)
- [Bedrock HTML Editor Documentation](../../../../../packages/prasso/bedrock-html-editor/README.md)
- [Church Package Documentation](../../../../../packages/prasso/church/README.md)
- [Messaging Package Documentation](../../../../../packages/prasso/messaging/README.md)

## Support

For issues or questions:
- Author: Bobbi Perreault
- Email: bcp@faxt.com
