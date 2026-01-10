# Domain Requirements: Acme Webshop

**Version:** 1.0  
**Last Updated:** 2026-01-09  
**Purpose:** EXAMPLE TEMPLATE FILE - Shows the structure of project-specific domain knowledge (filename has "-EXAMPLE" suffix)

---

## ⚠️ CRITICAL: THIS IS EXAMPLE DATA

**This file has "-EXAMPLE" suffix and contains EXAMPLE/PLACEHOLDER content. It should NOT be treated as actual project context.**

- **Filename suffix "-EXAMPLE" makes it clear this is a template** - agents will ignore files with this suffix
- **This is a template file** showing what type of content should go in project-context files
- **"Acme Webshop" is a placeholder example** - it is NOT a real project
- **Agents MUST NOT use this example data** to inform decisions or implementations
- **Create your own file** (e.g., `domain-requirements.md` without "-EXAMPLE") with your actual project's domain knowledge

**Before using agents, you MUST:**

1. Create your own `domain-requirements.md` (or similar filename) with your actual project's domain requirements, OR
2. Delete this example file and create your own project-context files

**Agents will ignore files with "-EXAMPLE" suffix. This file is for reference only - copy the structure, not the content.**

---

> **📝 Note:** This is an example file showing the type of project-specific context that should be stored in `docs/project-context/`. Replace this content with your actual project's domain knowledge, business rules, requirements, and context.

> **⚠️ READ-ONLY:** This file is in a READ-ONLY folder. Agents will NOT automatically maintain or update this file unless explicitly requested. You (the user) are responsible for keeping this file current, or explicitly requesting agent updates when context changes.

---

## Business Overview

Acme Webshop is an e-commerce platform specializing in artisanal products. The business focuses on high-quality, handmade items from independent creators.

### Target Market

- **Primary:** Urban professionals, ages 28-45, with disposable income for quality products
- **Secondary:** Gift buyers looking for unique items
- **Tertiary:** Collectors seeking limited edition items

### Business Model

- Commission-based: 15% commission on all sales
- Listing fees: $2.99 per product listing (renewed monthly)
- Premium seller tier: $29.99/month for enhanced listings and priority support

---

## Core Business Rules

### Product Requirements

1. **Product Approval Process:**

   - All new products require manual approval by admin team
   - Approval must happen within 24 hours of submission
   - Products must meet quality standards (handmade, artisanal, or unique vintage)
   - Rejected products must include feedback explaining rejection

2. **Product Listing Rules:**

   - Minimum 3 product images required
   - Product descriptions must be at least 100 characters
   - Product tags must include at least one category tag
   - All prices must be in USD (no international pricing yet)

3. **Inventory Management:**
   - Products can be "In Stock" or "Out of Stock"
   - Sellers must update inventory within 48 hours of sale
   - Low stock alerts trigger at 5 units remaining

### Order Processing Rules

1. **Order Fulfillment:**

   - Orders must be fulfilled within 7 business days
   - Sellers receive order notification immediately upon purchase
   - Tracking numbers must be provided within 2 business days of shipment

2. **Return Policy:**

   - Customers have 30 days from delivery to initiate return
   - Returns are free if item is defective or incorrect
   - Customers pay return shipping for "changed mind" returns
   - Refunds processed within 5 business days of return receipt

3. **Commission and Payment:**
   - Platform commission (15%) deducted at time of sale
   - Seller payments processed weekly (every Monday)
   - Minimum payout amount: $50 (balances below this roll over)
   - Payment method: ACH transfer or PayPal

### Customer Account Rules

1. **Account Creation:**

   - Email verification required
   - Password must be 8+ characters with one number and one special character
   - Guest checkout available (email required for order confirmation)

2. **Wishlist:**

   - Unlimited items per wishlist
   - Wishlist items send price drop notifications
   - Wishlist items persist across sessions for logged-in users

3. **Reviews and Ratings:**
   - Reviews can only be left 7 days after delivery
   - Reviews require at least 50 characters
   - Rating is 1-5 stars
   - One review per product per customer
   - Sellers can respond to reviews (response visible below review)

---

## Domain-Specific Terminology

### Product Terms

- **Variant:** Different options for the same product (e.g., size, color, material)
- **SKU:** Stock Keeping Unit - unique identifier for each product variant
- **Collection:** Curated group of products (e.g., "Holiday Gift Guide")
- **Maker:** Term used for sellers/creators on the platform

### Order Terms

- **Cart Abandonment:** When customer adds items to cart but doesn't complete checkout
- **Fulfillment Window:** 7 business days from order to shipment
- **Hold Period:** 3-day hold on payments before processing to seller account
- **Chargeback:** Disputed payment through payment processor

### User Roles

- **Customer:** Standard user who can browse and purchase
- **Maker:** User who can list and sell products
- **Admin:** Platform administrator with full access
- **Moderator:** Admin with limited access (product approval, customer service)

---

## Integration Requirements

### Payment Processing

- Primary processor: Stripe (credit cards, debit cards)
- Secondary: PayPal (customer preference option)
- Future: Apple Pay, Google Pay (Q2 2026)

### Shipping Integration

- ShipStation for label generation
- USPS, FedEx, UPS carrier integrations
- International shipping: Planned for Q3 2026 (currently US-only)

### Email Service

- Transactional emails: SendGrid
- Marketing emails: Mailchimp (opt-in required)
- Email templates: Must include unsubscribe link and business address

---

## Compliance and Legal

### Data Protection

- GDPR compliance required (EU customers)
- CCPA compliance required (California customers)
- Payment card data: PCI DSS Level 1 compliant (handled by Stripe)

### Tax Requirements

- Sales tax calculated at checkout based on delivery address
- Tax rates: Integrated with Avalara tax service
- Tax-exempt organizations: Supported with proper documentation

### Content Policy

- Products must not violate intellectual property rights
- No prohibited items (alcohol, tobacco, weapons, etc.)
- All product images must be original or licensed
- User-generated content (reviews) must comply with community guidelines

---

## Future Roadmap (Context for Planning)

### Q2 2026

- Mobile app (iOS and Android)
- International shipping expansion
- Seller analytics dashboard

### Q3 2026

- Subscription boxes (recurring product delivery)
- Affiliate program
- Enhanced search with AI recommendations

### Q4 2026

- Multi-vendor marketplace features
- Advanced seller tools (inventory forecasting, pricing suggestions)
- B2B wholesale channel

---

## Success Metrics

### Business KPIs

- **Gross Merchandise Value (GMV):** Target $500K/month by end of 2026
- **Average Order Value (AOV):** Target $75
- **Cart Abandonment Rate:** Target <60%
- **Customer Lifetime Value (CLV):** Target $250

### Operational Metrics

- **Order Fulfillment Time:** Target <5 business days average
- **Customer Service Response:** Target <24 hours
- **Product Approval Time:** Target <12 hours
- **Payment Processing Time:** Target same-day for weekly payouts

---

## Notes

- This document should be updated when business rules change
- Domain terminology should be consistent across all documentation
- Integration details should reference this document for context
- New features should check this document for business rule compliance
