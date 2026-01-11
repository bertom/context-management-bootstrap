# System Summary: [YOUR PROJECT NAME]

**Version:** 1.1  
**Last Updated:** 2026-01-10  
**Purpose:** Living system documentation that tracks changes and documents system-level decisions, trade-offs, and rationale for [YOUR PROJECT NAME]. Briefs contain detailed implementation context - SYSTEM_SUMMARY focuses on system-wide impact and architectural decisions.

> **⚠️ TEMPLATE:** This is a template. Replace "[YOUR PROJECT NAME]" with your actual project name (e.g., "Acme Webshop", "Mobile API", "Dashboard Service"). This document tracks changes to YOUR PROJECT, not the context management framework.

> **📝 Self-Updating Document:** This document maintains its own changelog and version history. Every change to [YOUR PROJECT NAME] or this document should be recorded in the [Document Changelog](#document-changelog) section below.

---

## Document Changelog

This document maintains a complete history of all changes, updates, and improvements. Each entry includes: what changed (brief summary), reference to the brief for implementation details, and system-level decisions/rationale (if applicable).

**Documentation Approach:**
- **Brief-level details:** Implementation specifics are documented in briefs (see "Brief Reference" in each entry)
- **System-level decisions:** Trade-offs, architectural decisions, and rationale that affect the system are documented here
- This avoids duplication: briefs contain detailed "what" and "why", SYSTEM_SUMMARY focuses on system-wide impact and architectural decisions

### Version 1.0 - 2026-01-09
**Status:** Initial System Summary

**What Changed:**
- Initialized system summary for [YOUR PROJECT NAME]
- Established changelog structure
- Documented initial architecture and components

**Brief Reference:** [N/A - Initial setup]

**System-Level Decisions:**
- Decision: Established SYSTEM_SUMMARY.md as living documentation that tracks system-level decisions
- Rationale: Need a single source of truth for system state that aggregates architectural decisions over time, separate from implementation details in briefs
- Impact: Enables tracking architectural evolution and decision rationale without duplicating brief content

[Replace this entry with your actual first change when you start using this template]

---

## Table of Contents

1. [Document Changelog](#document-changelog)
2. [System Overview](#system-overview)
3. [Architecture](#architecture)
4. [Agent Roles](#agent-roles)
5. [Documentation Structure](#documentation-structure)
6. [Workflow Patterns](#workflow-patterns)
7. [Maintenance Rules](#maintenance-rules)

---

## System Overview

### Purpose

[YOUR PROJECT NAME] is [describe your project's purpose and what it does]. 

**Example (Webshop):**
Acme Webshop is an e-commerce platform that enables online retail sales. It provides product catalog management, shopping cart functionality, checkout processing, order management, and customer account features.

### Core Components

[Replace with your actual system components. For a webshop:]

- **Frontend Application**: React-based web application serving customer and admin interfaces
- **Backend API**: Node.js REST API providing business logic and data access
- **Database**: PostgreSQL database storing products, orders, users, and inventory
- **Payment Gateway**: Stripe integration for secure payment processing
- **Inventory Management**: Real-time stock tracking and management system
- **Order Processing**: Order lifecycle management from placement to fulfillment
- **Authentication System**: User authentication and authorization (JWT-based)
- **Email Service**: Transactional email service for order confirmations and notifications

---

## Architecture

### System Architecture

[Replace with your actual system architecture. For a webshop:]

```
┌─────────────────┐
│   Frontend      │  React SPA (Customer + Admin)
│   (React)       │
└────────┬────────┘
         │ HTTP/REST
┌────────▼────────┐
│   Backend API   │  Node.js + Express
│   (Node.js)     │
└────────┬────────┘
         │
    ┌────┴────┬──────────────┬─────────────┐
    │         │              │             │
┌───▼───┐ ┌──▼───┐    ┌─────▼─────┐ ┌────▼────┐
│Postgres│ │Redis │    │   Stripe  │ │  Email  │
│   DB   │ │Cache │    │  Gateway  │ │ Service │
└────────┘ └──────┘    └───────────┘ └─────────┘
```

### Technology Stack

[Replace with your actual tech stack:]

**Frontend:**
- React 18.x
- TypeScript
- Tailwind CSS
- React Router
- Axios for API calls

**Backend:**
- Node.js 20.x
- Express.js
- TypeScript
- Prisma ORM
- JWT authentication

**Database:**
- PostgreSQL 15
- Redis for caching

**Services:**
- Stripe API for payments
- SendGrid for transactional emails
- AWS S3 for product images

### Key Modules

[Replace with your actual modules/components:]

1. **Product Catalog Module**: Product CRUD, search, filtering, categorization
2. **Shopping Cart Module**: Cart management, session persistence, cart calculations
3. **Checkout Module**: Order creation, payment processing, order confirmation
4. **Order Management Module**: Order tracking, status updates, fulfillment
5. **User Management Module**: Authentication, authorization, profile management
6. **Inventory Module**: Stock tracking, low stock alerts, inventory updates
7. **Admin Panel Module**: Product management, order processing, analytics dashboard

---

## Key Features and Modules

[Replace with your actual features. For a webshop:]

### Product Catalog

**Purpose:** Manage and display product information to customers

**Components:**
- Product database schema (products, categories, variants, images)
- Product search and filtering (full-text search, category filters, price range)
- Product detail pages with reviews and ratings
- Product recommendation engine

**API Endpoints:**
- `GET /api/products` - List products with filters
- `GET /api/products/:id` - Get product details
- `GET /api/products/search` - Search products
- `GET /api/categories` - List product categories

### Shopping Cart

**Purpose:** Manage customer shopping carts and cart persistence

**Components:**
- Cart session management (guest and authenticated users)
- Cart calculations (subtotal, tax, shipping, discounts)
- Cart persistence across sessions
- Cart item quantity management

**API Endpoints:**
- `GET /api/cart` - Get current cart
- `POST /api/cart/items` - Add item to cart
- `PUT /api/cart/items/:id` - Update cart item
- `DELETE /api/cart/items/:id` - Remove cart item
- `POST /api/cart/apply-coupon` - Apply discount code

### Checkout and Payment

**Purpose:** Process orders and handle payments

**Components:**
- Order creation workflow
- Address validation
- Payment processing via Stripe
- Order confirmation and email notifications

**API Endpoints:**
- `POST /api/checkout` - Create order
- `POST /api/payments/process` - Process payment
- `GET /api/orders/:id` - Get order details

[Continue with other key features...]

---

## Data Models

[Replace with your actual data models. For a webshop:]

### Core Entities

**Product:**
- id, name, description, sku
- price, compareAtPrice, cost
- inventoryQuantity, trackInventory
- categoryId, tags
- images (array)
- status (active/inactive/draft)

**Order:**
- id, orderNumber, userId
- status (pending/processing/shipped/delivered/cancelled)
- subtotal, tax, shipping, discount, total
- shippingAddress, billingAddress
- paymentStatus, paymentMethod
- createdAt, updatedAt

**Cart:**
- sessionId, userId (nullable)
- items (array of cart items)
- couponCode, discountAmount
- expiresAt

**User:**
- id, email, passwordHash
- firstName, lastName
- phone, addresses (array)
- role (customer/admin)
- createdAt, lastLoginAt

[Continue with other data models...]

### Documentation Maintenance Rules

**MANDATORY:** When updating ANY documentation file:

1. Update "Last Updated" date (YYYY-MM-DD format)
2. Increment version number (major/minor/patch)
3. Update both fields BEFORE or DURING the edit

**Changelog Entries:**
- Every system change gets a changelog entry
- Format: Version, Date, Status, What Changed, Why, Impact
- Entries are chronological (newest first)

**Validation:**
- SYSTEM_BUDDY validates documentation freshness
- Operator reviews documentation periodically
- Documentation drift is treated as system issue

---

## System Flows

[Replace with your actual system flows. For a webshop:]

### Order Processing Flow

1. Customer adds items to cart
2. Customer proceeds to checkout
3. System validates cart (stock, pricing)
4. Customer enters shipping address
5. System calculates shipping costs
6. Customer selects payment method
7. System creates order (pending status)
8. Payment processed via Stripe
9. Order status updated to "processing"
10. Order confirmation email sent
11. Inventory deducted
12. Admin processes order
13. Shipping label generated
14. Order status updated to "shipped"
15. Tracking email sent to customer
16. Customer receives order
17. Order status updated to "delivered"

### Product Search Flow

1. User enters search query
2. Query processed (normalized, tokenized)
3. Full-text search against product database
4. Results filtered by active status
5. Results sorted by relevance/price/rating
6. Pagination applied
7. Results returned to frontend
8. Frontend displays results with filters
9. User can apply additional filters
10. Results update dynamically

[Add other important system flows...]

---

## Dependencies

[Replace with your actual dependencies:]

**Runtime Dependencies:**
- Node.js 20.x
- PostgreSQL 15
- Redis 7.x

**External Services:**
- Stripe API (payment processing)
- SendGrid API (transactional emails)
- AWS S3 (image storage)
- CloudFront CDN (asset delivery)

**Development Dependencies:**
- TypeScript
- Jest (testing)
- ESLint (linting)
- Prettier (formatting)

## Deployment

[Replace with your actual deployment information:]

**Environments:**
- Development (local)
- Staging (staging.example.com)
- Production (example.com)

**Deployment Process:**
1. Code merged to main branch
2. Automated tests run
3. Build artifacts created
4. Deploy to staging
5. Smoke tests on staging
6. Manual approval for production
7. Deploy to production
8. Post-deployment verification

**Infrastructure:**
- Frontend: Vercel/Netlify
- Backend: AWS ECS/Docker containers
- Database: AWS RDS PostgreSQL
- Cache: AWS ElastiCache Redis

---

## Changelog Maintenance Rules

> **Note for Agents:** When updating this document, you MUST add a changelog entry for every change to [YOUR PROJECT NAME].

**When to add entry:**
- Any system behavior change
- Architecture changes
- New features added
- Bug fixes
- Performance improvements
- Dependency updates

**Entry format:**
```markdown
### Version X.Y - YYYY-MM-DD
**Status:** [Enhancement | Fix | Redesign | Breaking]

**What Changed:**
- [Brief summary of what changed - concise, high-level]

**Brief Reference:**
- Brief: `work/briefs/archive/YYYY-MM-DD_name_brief.md`
- For detailed implementation context, decisions, and rationale, see the brief (brief is archived after implementation)

**System-Level Decisions:** (Only if brief contains "System-Level Decisions" section)
- Decision: [What system-level decision was made]
- Trade-off: [What was considered]
- Rationale: [Why this decision - extracted from brief's System-Level Decisions section]
- Impact: [How this affects system architecture/patterns/future work]

**Impact:**
- [What this affects - users, API, database, system architecture, etc.]

**Files Modified:**
- [List of files]
```

**Note:** If brief does NOT contain system-level decisions (standard implementation), the "System-Level Decisions" section can be omitted or state: "No system-level decisions - standard implementation."

**Documentation Updates:**
- Update USER_GUIDE.md if user-facing behavior changes
- Update this document for all changes
- Keep entries factual and clear
- Use this as single source of truth for [YOUR PROJECT NAME] system state

---

## Notes

- This document tracks [YOUR PROJECT NAME], not the context management framework
- Add project-specific sections as needed
- Maintain changelog discipline (every change gets entry)
- Keep entries factual and clear
- Use this as single source of truth for system state

