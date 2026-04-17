# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM (available, not yet used — products are in-memory)
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)

## CircuitCart

Full-stack electronics e-commerce web app for PC parts and laptop components.

### Features
- Splash screen on first load
- User signup/login (localStorage)
- Product grid with search, category/brand/price filters, sort
- Product detail with specs, reviews, price history chart
- Slide-in cart panel with quantity controls
- Checkout with form validation and payment method selection
- Order confirmation with delivery timeline
- PC Builder: select CPU/GPU/RAM/Motherboard, compatibility check (same brand = compatible)
- PC Builder: combined total price, add all to cart

### Architecture
- **Frontend**: React + Vite at `/` (circuit-cart artifact)
- **Backend**: Express API at `/api` (api-server artifact)
- **Products**: In-memory data in `artifacts/api-server/src/data/products.ts`
- **Cart**: In-memory session store in cart route
- **Orders**: In-memory store in orders route

### Key files
- `artifacts/circuit-cart/src/App.tsx` — Router with all pages
- `artifacts/circuit-cart/src/pages/` — All page components
- `artifacts/circuit-cart/src/components/` — Navbar, CartPanel, ProductCard, etc.
- `artifacts/circuit-cart/src/lib/cart-context.tsx` — Cart state + API mutations
- `artifacts/circuit-cart/src/lib/user-context.tsx` — User auth via localStorage
- `artifacts/api-server/src/routes/products.ts` — Product API routes
- `artifacts/api-server/src/routes/cart.ts` — Cart API routes  
- `artifacts/api-server/src/routes/orders.ts` — Checkout/orders routes
- `artifacts/api-server/src/data/products.ts` — 17 products across 7 categories
- `lib/api-spec/openapi.yaml` — OpenAPI spec (source of truth)

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally
- `pnpm --filter @workspace/circuit-cart run dev` — run frontend locally

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.
