# BeeNext Project Organization & Architecture

This document describes the directory structure, file organization, and architectural layout of the BeeNext ecosystem, which consists of a backend server (`BE_BeeNext`) and a cross-platform mobile client (`MOBILE_BeeNext`).

---

## 📂 Overall Repository Layout

```
BeeNext/
├── BE_BeeNext/         # Express + TypeScript + Prisma Backend
└── MOBILE_BeeNext/     # Flutter + Dart Mobile App
```

---

## 📱 Mobile App Organization (`MOBILE_BeeNext`)

The Flutter application code is grouped inside the `lib/` directory using a simplified, feature-grouped structure.

### `lib/` Structure

```
lib/
├── bloc/               # State Management (BLoC Pattern)
│   ├── auth_bloc/
│   ├── home_feed_bloc/
│   ├── listing_create_bloc/
│   ├── my_listings_bloc/
│   ├── product_detail_bloc/
│   ├── profile_bloc/
│   └── search_catalog_bloc/
│
├── data/               # Data Layer
│   ├── models/         # Data Models & Entities (e.g. auth_session.dart)
│   └── services/       # Network Services & Repository Implementations (e.g. api_client.dart)
│
├── helpers/            # Application Shared Helpers & Utils
│   ├── api_settings/   # API configuration and constant URLs
│   ├── di/             # Dependency Injection / Bloc Providers
│   ├── errors/         # Custom exceptions / network error handlers
│   ├── routes/         # Navigation Route generation maps
│   ├── theme/          # App look-and-feel theme definitions
│   └── utils/          # Standalone utilities (e.g. api_image_url.dart)
│
├── pages/              # Visual Screens
│   ├── auth/           # Login, Sign Up, Landing screens
│   ├── marketplace/    # Feed, Create Listing, Detail, Search pages
│   └── profile/        # User Profile settings page
│
├── widgets/            # Custom reusable widgets
│   ├── marketplace/    # Marketplace modals / cards
│   ├── profile/        # Profile modals / sheets
│   └── shared/         # Universal widgets (e.g. network image view)
│
├── app.dart            # Root Material App config
└── main.dart           # App entry point (initializes .env, shared preferences)
```

---

## 🖥️ Backend Service Organization (`BE_BeeNext`)

The Node.js Express server backend is structured using TypeScript and modular domain packaging.

### `src/` Structure

```
src/
├── config/             # Server port and DB connection keys loading
├── middlewares/        # Express request middle validation (e.g. JWT check)
├── modules/            # Domain Feature Modules
│   ├── assets/         # Static uploads and media handlers
│   ├── auth/           # Login, registration, profile updates (controller, service, repository, routes)
│   ├── categories/     # Listing categories definitions
│   ├── notifications/  # Action notifications system
│   ├── payments/       # Transaction checks
│   ├── products/       # Core product listing management
│   └── regions/        # Campus region coordinates and listings
│
├── types/              # TS custom type extensions (e.g. custom express request context)
├── utils/              # Base utility functions
└── index.ts            # Entrypoint file to bootstrap the Express server
```
