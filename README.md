# Laravel Multi-Vendor E-commerce Application

A production-grade marketplace built with Laravel 10 that lets multiple vendors manage inventory, orders, and payouts from a single, curated storefront. The project includes fully fledged admin and vendor panels, a responsive storefront, and an authenticated REST API powered by Laravel Passport.

## Table of Contents
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Architecture Highlights](#architecture-highlights)
- [Quick Start](#quick-start)
- [Database & Seed Data](#database--seed-data)
- [Running the App](#running-the-app)
- [API & Integrations](#api--integrations)
- [Testing](#testing)
- [Project Assets](#project-assets)
- [License](#license)

## Key Features
- **Marketplace Operations**
  - Multi-vendor onboarding with super-admin approval and guard-based authentication for admins, vendors, and shoppers.
  - Commission rules per vendor, vendor bank/business profiles, and role-based access (superadmin, admin, vendor, customer).
  - Dynamic sections, categories (multi-level), banners, breadcrumbs, and SEO/meta management.
- **Catalog & Discovery**
  - AJAX-driven product filters, faceted search (name, color, code), featured/new/best-seller listings, and recently viewed tracking.
  - Rich media support (images, videos, TinyMCE content editor) with Intervention Image processing, custom preloading screens, and dual favicons for admin/front panels.
- **Cart, Checkout & Payments**
  - Shiprocket integration for fulfillment plus webhook-powered stock sync.
  - PayPal and Iyzico gateways via Omnipay, Laravel Coupons (fixed/percentage, single/multi-use), and customizable shipping-charge matrix (weight, country, third-party rates).
  - Multiple delivery addresses, AJAX mini-cart, and comprehensive order logs/history.
- **Customer Experience**
  - Star ratings & reviews, newsletter subscriptions, offline SMS notifications, Mailtrap-ready transactional emails (registration, approvals, shipping updates), and EasyZoom-enhanced product galleries.
- **Admin Productivity**
  - DataTables-enhanced grids, extensive AJAX forms (password updates, validations, etc.), barcode/QR code generation for products, PDF invoices via Dompdf, CSV/XLS import-export with Laravel Excel, and rigorous regex-based validation rules.
- **Developer Experience**
  - Dedicated REST API secured by Laravel Passport, Laravel Sanctum support, webhook endpoints, PHP cURL integrations, and exhaustive database seeders for every core entity.

## Tech Stack
- **Backend:** PHP 8.1+, Laravel 10, Laravel Passport, Laravel Sanctum, Omnipay (PayPal), Iyzico SDK, Laravel Excel, Dompdf, Intervention Image, Milon Barcode.
- **Frontend:** Blade, jQuery, AJAX, Vite, Tailwind CSS, Alpine.js, DataTables, EasyZoom, SweetAlert2, TinyMCE.
- **Tooling:** Composer, NPM/Vite, PHPUnit, Laravel Pint, Laravel Sail (optional), Postman.
- **Infrastructure:** MySQL/MariaDB, Queue workers (database/redis compatible), Mail (Mailtrap/Mailgun/Postmark), SMS gateway (configured via vendor services).

## Architecture Highlights
- `app/Http/Controllers/Admin|Front|Auth|API` split for admin console, storefront, login flows, and REST API endpoints.
- `app/Models` encapsulates vendors, products, orders, filters, coupons, shipping, ratings, and newsletters.
- `database/seeders` pre-populates marketplace data; `Database - multivendor_ecommerce/` ships a ready-to-import SQL dump.
- `resources/views/admin|front` deliver bespoke layouts for storefront, vendor console, and admin dashboards.
- `Postman Collection of API Endpoints/` provides ready-made REST requests.
- `Project Screenshots/` showcases primary workflows (frontend, admin, checkout, inventory).

## Quick Start
1. Clone the repository and install dependencies:
   ```bash
   git clone https://github.com/<your-org>/laravel-multi-vendor-e-commerce-application.git
   cd laravel-multi-vendor-e-commerce-application
   composer install
   npm install
   ```
2. Create your environment file:
   ```bash
   cp .env.example .env    # If .env.example is missing, duplicate from a fresh Laravel 10 install.
   ```
3. Configure `.env`:
   - Database connection (`DB_*`), cache, queue, session.
   - Mail driver/credentials (Mailtrap by default).
   - Payment credentials (`PAYPAL_*`, `IYZICO_*`) and SMS gateway keys.
   - Shiprocket API keys, storage, and other third-party tokens.
4. Generate the application key and link storage:
   ```bash
   php artisan key:generate
   php artisan storage:link
   ```
5. Run database migrations and seeders:
   ```bash
   php artisan migrate --seed
   ```
6. Install Laravel Passport keys:
   ```bash
   php artisan passport:install
   ```

## Database & Seed Data
- Seeders create super-admin, vendor accounts, catalog, coupons, shipping tables, filters, newsletter subscribers, ratings, and order statuses automatically.
- A full SQL dump lives in `Database - multivendor_ecommerce/multivendor_ecommerce database - SQL Dump File - phpMyAdmin Export.sql` if you prefer importing data directly.
- Default credentials after seeding:
  - Super Admin: `admin@admin.com` / `123456`
  - Vendor Admin: `john@admin.com` / `123456`
  - Additional customers, filters, and demo content are populated via dedicated seeders.

## Running the App
```bash
# Start the API/web server
php artisan serve

# Compile frontend assets
npm run dev          # or: npm run build && npm run preview for production bundles
```
- Configure a queue worker (`php artisan queue:work`) if you enable queued emails/SMS or webhook jobs.
- Schedule tasks (cron) to trigger `php artisan schedule:run` for routine cleanup if required.

## API & Integrations
- OAuth2 authentication with Laravel Passport (`/oauth/token`) protects all API routes under `routes/api.php`.
- Import the Postman collection located at `Postman Collection of API Endpoints/Multi-vendor E-commerce Application API.postman_collection.json`.
- Webhooks update inventory in real time; ensure your third-party services call the exposed webhook endpoints with valid signatures.
- External services leveraged:
  - Shiprocket for shipping rates and status updates.
  - PayPal and Iyzico payment gateways via Omnipay.
  - Mailtrap (default) or other SMTP providers for transactional mail.
  - SMS gateway for offline messaging.

## Testing
- Feature and unit tests live in `tests/Feature` and `tests/Unit`.
- Run the full suite:
  ```bash
  php artisan test
  ```
- Use `php artisan test --filter=Auth` to focus on authentication scenarios, or `phpunit` for raw PHPUnit runs.
- Laravel Pint is available for code style checks (`./vendor/bin/pint`).

## Project Assets
- High-level tour images in `Project Screenshots/` cover storefront, admin dashboard, product management, checkout, and cart flows.
- Frontend assets are served via Vite from `resources/js` and `resources/css`; compiled bundles publish to `public/front` and `public/admin`.

## License
This project is released under the MIT License. See the `LICENSE` file for details.

## Contact
For questions or support, reach out to Opada Aljondi at `opada.m.aljondi@gmail.com`.
