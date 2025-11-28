# ShopHub - E-Commerce Marketplace

## Overview

ShopHub is a general marketplace e-commerce platform built as a full-stack web application. It allows users to browse and purchase products across multiple categories (electronics, fashion, home & garden, sports, beauty, books & media), manage shopping carts, and complete orders. The platform includes admin capabilities for managing products, categories, and orders.

**Tech Stack:**
- **Frontend**: React with TypeScript, Wouter for routing, TanStack Query for data fetching
- **Backend**: Express.js with TypeScript
- **Database**: PostgreSQL via Neon serverless with Drizzle ORM
- **UI**: Shadcn/ui components with Tailwind CSS
- **Authentication**: Replit Auth (OpenID Connect) with Passport.js
- **Build**: Vite for frontend, ESBuild for server bundling

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Component-Based React Application** using functional components with hooks. The architecture follows a feature-based organization:

- **Pages**: Route-level components (`Landing`, `Home`, `Products`, `ProductDetail`, `Category`, `Checkout`, `Orders`, admin pages)
- **Shared Components**: Reusable UI building blocks organized by domain (`layout/Header`, `products/ProductCard`, `cart/CartSheet`)
- **UI Components**: Shadcn/ui component library providing consistent, accessible primitives
- **State Management**: TanStack Query for server state, React hooks for local state
- **Routing**: Wouter for lightweight client-side routing
- **Styling**: Tailwind CSS with custom design system extending Shadcn's "new-york" style

**Design Philosophy**: Product-first presentation inspired by modern e-commerce platforms (Shopify, Amazon), emphasizing clear conversion paths and trustworthy interface patterns. The design uses Inter font family, responsive grid layouts (2/3/4 columns), and consistent spacing primitives.

**Authentication Flow**: Server-side session with client-side state synchronization via TanStack Query. Unauthenticated users see a `Landing` page, authenticated users see the main `Home` page.

### Backend Architecture

**Express.js REST API** with TypeScript using a layered architecture:

1. **Route Layer** (`routes.ts`): Defines HTTP endpoints, applies middleware (authentication, admin checks), validates inputs using Zod schemas
2. **Storage Layer** (`storage.ts`): Abstracts database operations, provides type-safe data access methods
3. **Database Layer** (`db.ts`): Manages PostgreSQL connection pool via Neon serverless

**Key Architectural Decisions**:
- **Session-based Authentication**: Uses Replit Auth (OpenID Connect) with PostgreSQL session storage via `connect-pg-simple`, providing secure server-side sessions
- **Middleware Pattern**: Authentication middleware (`isAuthenticated`, `isAdmin`) applied at route level for access control
- **Type Safety**: Shared schema types between frontend and backend via `@shared/schema` imports
- **Error Handling**: Centralized error responses with appropriate HTTP status codes
- **Build Strategy**: Server code bundled with ESBuild, selective dependency bundling to reduce cold start times

**API Structure**:
- `/api/auth/*` - Authentication endpoints
- `/api/categories/*` - Category CRUD operations
- `/api/products/*` - Product listing, filtering, and management
- `/api/cart/*` - Shopping cart operations
- `/api/orders/*` - Order creation and management

### Database Architecture

**PostgreSQL with Drizzle ORM** providing type-safe database access. Schema design supports a general marketplace with flexible product types:

**Core Tables**:
- `users` - User profiles with admin flag, integrated with Replit Auth
- `categories` - Hierarchical categories (parent-child relationships via `parentId`)
- `products` - Main product catalog with fields for pricing, inventory, images (JSON array), brand, SKU
- `product_variants` - Product variations (size, color) with independent pricing and stock
- `carts` - User shopping carts
- `cart_items` - Cart line items linking products/variants with quantities
- `orders` - Order records with status tracking, shipping details, totals
- `order_items` - Order line items preserving product details at time of purchase
- `sessions` - Server-side session storage for authentication

**Design Decisions**:
- **Soft Schema for Product Types**: Single `products` table with optional fields supports physical products (weight, dimensions), digital products, and subscriptions without rigid type hierarchies
- **Image Storage**: Product images stored as JSON array of URLs (external CDN/storage assumed)
- **Denormalization in Orders**: Order items store product name/price to maintain historical accuracy even if products change
- **Hierarchical Categories**: `parentId` foreign key enables parent-child category relationships for better organization
- **Decimal Pricing**: Uses `decimal` type for accurate monetary calculations

**Relationships**:
- Products → Categories (many-to-one)
- Products → Variants (one-to-many)
- Carts → CartItems → Products (many-to-many through junction)
- Orders → OrderItems → Products (many-to-many through junction)

### External Dependencies

**Authentication**: Replit Auth (OpenID Connect) - Provides user identity and session management. The app uses `openid-client` and `passport` for OAuth2/OIDC integration.

**Database**: Neon Serverless PostgreSQL - Managed PostgreSQL with WebSocket connection pooling via `@neondatabase/serverless`.

**UI Framework**: Shadcn/ui with Radix UI primitives - Provides accessible, customizable components. Uses 30+ Radix UI primitives (@radix-ui/react-*).

**CSS Framework**: Tailwind CSS with PostCSS - Utility-first styling with custom design tokens defined in `tailwind.config.ts`.

**Form Handling**: React Hook Form with Zod validation - Type-safe form management using `@hookform/resolvers` and `zod` schemas.

**Build Tools**: 
- Vite - Frontend dev server and production bundler
- ESBuild - Server-side code bundling
- Drizzle Kit - Database schema migrations

**Development Tools** (Replit-specific):
- `@replit/vite-plugin-cartographer` - Development navigation
- `@replit/vite-plugin-dev-banner` - Development environment indicators
- `@replit/vite-plugin-runtime-error-modal` - Enhanced error reporting

**Session Storage**: PostgreSQL-backed sessions via `connect-pg-simple`, avoiding memory store limitations in distributed environments.

**Type Generation**: Drizzle ORM auto-generates TypeScript types from database schema, ensuring type safety across the stack via `drizzle-zod` integration.