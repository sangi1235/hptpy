# E-Commerce Marketplace Design Guidelines

## Design Approach
**Reference-Based**: Drawing from modern e-commerce leaders (Shopify, Amazon, Stripe) with emphasis on product-first presentation, clear conversion paths, and trustworthy interface patterns.

**Core Principle**: Balance visual appeal with functional clarity—customers need to browse easily, trust the platform, and complete purchases without friction.

---

## Typography System

**Font Stack**: Inter or System UI for clean, professional readability
- **Headings**: 2xl to 4xl, font-semibold to font-bold
- **Product Titles**: lg to xl, font-medium
- **Body Text**: base (16px), font-normal
- **Price**: lg to 2xl, font-bold for emphasis
- **Labels/Meta**: sm to xs, font-medium, uppercase for category tags

---

## Layout & Spacing System

**Spacing Primitives**: Use Tailwind units of 2, 4, 6, 8, 12, 16, 24
- **Component padding**: p-4 to p-6 for cards, p-8 for sections
- **Section spacing**: py-12 to py-16 for desktop, py-8 for mobile
- **Grid gaps**: gap-4 for tight grids, gap-6 to gap-8 for product layouts
- **Container**: max-w-7xl with px-4 to px-8

**Product Grid**: 
- Mobile: 2 columns (grid-cols-2)
- Tablet: 3 columns (md:grid-cols-3)
- Desktop: 4 columns (lg:grid-cols-4)

---

## Component Library

### Navigation Header
- Sticky header with three-tier structure:
  1. **Top bar**: Minimal height (h-10), small text for shipping/returns info
  2. **Main header**: Logo left, search bar center (max-w-2xl), account/cart icons right
  3. **Category nav**: Horizontal scrollable category pills or dropdown mega-menu

### Product Cards
- Aspect ratio: square (aspect-square) for images
- Structure: Image → Title (2 lines max) → Price → Rating stars
- Hover state: Subtle lift (transform scale-105) and shadow increase
- Quick add-to-cart button appears on hover
- Border: border with rounded corners (rounded-lg)

### Search & Filters
- Sidebar filters (desktop): sticky position, w-64
- Mobile filters: slide-in drawer
- Filter groups: collapsible sections with checkbox lists
- Active filters: pill badges with remove option above results

### Shopping Cart (Slide-over)
- Fixed right overlay (w-96)
- Product rows: thumbnail (w-20) + details + quantity selector + remove
- Sticky footer: subtotal + checkout button (w-full, prominent)
- Empty state: centered icon + message + "Continue Shopping" link

### Product Detail Page
- Two-column layout (lg:grid-cols-2)
- Left: Image gallery with thumbnails + main image lightbox
- Right: Title → Price → Rating/Reviews count → Size/variant selectors → Add to cart CTA → Accordion details (Description, Shipping, Returns)

### Checkout Flow
- Multi-step progress indicator at top
- Single-column form (max-w-2xl mx-auto)
- Order summary sidebar (sticky on desktop)
- Large, clear CTAs at each step

### Admin Dashboard
- Sidebar navigation (w-64, hidden on mobile)
- Data tables with sortable columns
- Action buttons in each row
- Modal forms for create/edit operations
- Stats cards grid at top (grid-cols-4)

---

## Images

**Hero Section**: Full-width banner (h-96 to h-screen/2) showcasing featured products or seasonal campaign with category CTAs overlaid. Use lifestyle product photography with blurred-background buttons.

**Product Images**: High-quality, consistent white or minimal backgrounds. Multiple angles for detail pages.

**Category Images**: Banner-style headers for category pages (h-48 to h-64)

---

## Key Interactions

- **Add to Cart**: Toast notification bottom-right confirming addition
- **Quantity Selectors**: Plus/minus buttons with input field
- **Image Zoom**: Click to expand in lightbox modal
- **Loading States**: Skeleton screens for product grids
- **Form Validation**: Inline error messages below inputs

---

## Trust Elements

- Security badges near payment inputs
- Customer review stars prominently on product cards
- Free shipping threshold indicator in cart
- Clear return policy links
- Professional product photography throughout

**Hierarchy Priority**: Product discovery → Easy adding to cart → Frictionless checkout → Post-purchase confidence