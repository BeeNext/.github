# BeeNext Project Organization

BeeNext is split into two main applications:

- `BE_BeeNext` - Express + TypeScript backend API
- `MOBILE_BeeNext` - Flutter mobile client

The project follows a simple feature-first structure. Backend code is grouped by API domain, while mobile code is grouped by application layer and screen feature.

---

## Backend Organization

The backend is organized around Express route modules. Each module owns its controller, service, repository, and route file when needed.

```text
BE_BeeNext/
|-- prisma/
|   |-- schema.prisma
|   |-- seed.ts
|   `-- migrations/
|-- src/
|   |-- config/
|   |-- middlewares/
|   |-- modules/
|   |   |-- assets/
|   |   |-- auth/
|   |   |-- categories/
|   |   |-- notifications/
|   |   |-- products/
|   |   `-- regions/
|   |-- types/
|   |-- utils/
|   `-- index.ts
|-- package.json
`-- tsconfig.json
```

### Backend Layers

| Layer | Purpose |
| --- | --- |
| `routes` | Defines Express endpoints and middleware chain |
| `controller` | Reads request data, validates basic input, returns HTTP responses |
| `service` | Holds business rules and cross-repository workflow |
| `repository` | Talks directly to Prisma/database |
| `types` | Shared TypeScript request, response, product, auth, and notification types |
| `utils` | Common helpers for responses, storage, parsing, JWT, and passwords |

### Backend Domains

| Module | Responsibility |
| --- | --- |
| `assets` | Serve stored image assets |
| `auth` | Register, login, current user profile, password and phone updates |
| `categories` | Product category list |
| `notifications` | User marketplace notification feed |
| `products` | Product list, detail, create, edit, delete, and owner listings |
| `regions` | BINUS campus region list |

---

## Mobile Organization

The Flutter app separates state management, data access, helpers, pages, and reusable widgets.

```text
MOBILE_BeeNext/
|-- assets/
|   |-- fonts/
|   |-- icons/
|   `-- illustrations/
|-- lib/
|   |-- bloc/
|   |-- data/
|   |-- helpers/
|   |-- pages/
|   |-- widgets/
|   |-- app.dart
|   `-- main.dart
|-- pubspec.yaml
`-- test/
```

### Mobile Layers

| Layer | Purpose |
| --- | --- |
| `bloc` | UI state and async workflow orchestration |
| `data/models` | App data models, such as auth session and user |
| `data/services` | REST API client, remote data sources, repository interfaces, implementations |
| `helpers/api_settings` | API base URL and endpoint constants |
| `helpers/di` | Repository and dependency providers |
| `helpers/errors` | App-level exception types |
| `helpers/routes` | App route generation |
| `helpers/theme` | Shared Material theme |
| `helpers/utils` | Small reusable helpers, such as API image URL resolution |
| `pages` | Full-screen UI flows |
| `widgets` | Reusable smaller UI components |

### Mobile Feature Areas

| Area | Files |
| --- | --- |
| Auth | `pages/auth`, `bloc/auth_bloc`, auth services |
| Home Feed | `pages/marketplace/home_page.dart`, `bloc/home_feed_bloc` |
| Search | `pages/marketplace/search_page.dart`, `bloc/search_catalog_bloc` |
| Product Detail | `pages/marketplace/detail_page.dart`, `bloc/product_detail_bloc` |
| Create/Edit Listing | `pages/marketplace/add_page.dart`, `bloc/listing_create_bloc` |
| My Listings | `pages/marketplace/my_listings_page.dart`, `bloc/my_listings_bloc` |
| Notifications | `pages/marketplace/notification_page.dart` |
| Profile | `pages/profile`, `bloc/profile_bloc`, profile widgets |

---

## Request Flow

### Backend Request Flow

```text
HTTP request
-> route
-> middleware
-> controller
-> service
-> repository
-> Prisma/PostgreSQL
-> response helper
-> HTTP response
```

### Mobile Data Flow

```text
Page widget
-> BLoC event
-> repository
-> remote data source
-> ApiClient
-> backend API
-> BLoC state
-> page rebuild
```

---

## Documentation Style

The project documentation follows a compact README style:

- Start with what the project does.
- List the tech stack.
- Show setup and environment variables.
- Document useful scripts.
- Keep endpoint/features tables short and practical.
- Use ASCII tree diagrams to avoid encoding issues across editors.
