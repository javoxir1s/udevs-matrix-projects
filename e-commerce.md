# E-Commerce — Technical Requirements

---

## From: Client
## To: Development Team

---

## What I Want

I need a full-fledged online store. Not a template, not a half-baked MVP — a working product that people can actually use. A customer comes in, picks a product, selects a size/color, adds it to the cart, pays, and tracks the delivery. As the owner, I see all orders, manage the catalog, and understand whether I'm making money or not.

---

## Roles & Access

I need 4 roles. Each role only sees what's relevant — no extra buttons or pages.

**SuperAdmin** — that's me. I see everything: products, orders, users, finances. I can assign roles to other users. I see profit and loss.

**Content Manager** — the person who manages the catalog. Creates categories, adds products, uploads photos, writes descriptions, sets prices. Cannot see finances or change order statuses.

**WareHouse Admin** — warehouse manager. Sees orders, changes delivery statuses (packed → shipped → delivered). Manages stock levels. Cannot edit the catalog or see finances.

**Client** — the buyer. Registers, browses the catalog, adds to cart, places an order, pays, tracks the status, leaves reviews.

Authentication — JWT tokens (access + refresh). Passwords hashed with bcrypt. Refresh token renews the access token without re-login.

---

## Product Catalog

I need a category system — tree structure: category → subcategory. For example: "Clothing" → "Men's" → "Jackets".

The product listing must support:
- Filtering by: category, price (min–max), brand, rating, stock availability
- Sorting by: price (asc/desc), popularity, rating, newest
- Search by product name
- Pagination (don't load all 10,000 products at once)

Product card in the catalog shows: photo, name, price (if discounted — old and new price), rating, "Out of Stock" badge if stock = 0.

---

## Products & Variations

This is a key point — a product is not just one item. A product has **variations**.

Example: "Nike Air" t-shirt is one product. But it has:
- Sizes: S, M, L, XL
- Colors: black, white, red

Each combination (S + black, M + white, etc.) is a **separate variation (SKU)**. Each variation has its own:
- SKU code (unique identifier)
- Price (may differ from the base — e.g. XL costs more)
- Stock quantity (`stock_qty`) — separate for each variation
- Its own photos (black t-shirt — one set of photos, white — another)

A product also has attributes (specifications): weight, material, country of origin, warranty, etc. These are displayed in a specs table.

---

## Product Detail Page

When the customer clicks on a product card, they land on the detail page. Here's what I want to see:

- **Breadcrumbs** — navigation: Home > Clothing > Men's > Jackets
- **Photo gallery** — main photo + thumbnails; when the variation changes (color), photos update
- **Name, brand**
- **Price** — if discounted, show old price crossed out and the new one
- **Variation selector** — color buttons, size dropdown. When variation changes, the following update: price, photos, availability
- **Stock status** — "In Stock" / "Low Stock" (< 5 pcs) / "Out of Stock" — for the selected variation
- **Product description** — rich text
- **Specifications table** — weight, material, dimensions, etc.
- **Rating and reviews** — average score, review count, list of reviews with name, date, text, score
- **"Add to Cart" button** — disabled when the selected variation is out of stock
- **"Similar Products" block** — products from the same category

---

## Cart

- Each cart item is tied to a specific variation (SKU), not just the product. If I added "Nike Air, black, L" — that exact variation is in the cart
- Can change quantity, remove items
- Displays: photo, name, variation, unit price, quantity, line total
- Bottom — grand total and item count
- Cart persists for logged-in users (not lost on page reload)

---

## Checkout

- Delivery address, phone number, order comment
- On checkout — the system checks `stock_qty` for each variation. If something is insufficient — show an error specifying which variation is short
- On success — deduct `stock_qty`
- Save the price at the time of order (`price_at_order`) — so if the price changes tomorrow, the order keeps the old price
- Order contains: user, line items (variation + qty + price_at_order), total, delivery address, comment

---

## Payment

No real payment gateway needed — emulation. But the logic must be complete:
- Statuses: `pending` → `paid` → `failed` → `refunded`
- After payment, the order transitions from `new` to `paid`

---

## Order Status

Order lifecycle: `new` → `paid` → `processing` → `shipped` → `delivered` → `cancelled`

Each transition is saved to history: timestamp, who changed it, comment. Only SuperAdmin or WareHouse Admin can change the status.

The customer sees the current status and full transition history as a timeline.

---

## Reviews & Ratings

- Only after `delivered` status can the customer leave a review
- Rating 1–5, text comment
- Only verified buyers can review (those who actually purchased)
- Average rating displayed on the product card and detail page

---

## Profit / Loss

This section is SuperAdmin only. I need to understand — am I making money or losing it.

- Each variation has a `cost_price` (what I paid for it) and `sell_price` (what I sell it for)
- Profit per order = sum of (sell_price - cost_price) across all line items
- Summary: revenue (all sales), cost (all expenses), net profit/loss
- Filter by period: day, week, month, custom date range
- Clearly show: are we **in profit** or **at a loss**

---

## ERD (Database Diagram)

Before development starts, I need an ERD diagram of the entire database. All tables, relationships, data types. Use dbdiagram.io, drawSQL, or Mermaid. Include in project documentation.

---

## Frontend — Pages I Need

- **Home page** — banners, popular products, categories
- **Catalog** — product cards, filters, sorting, search, pagination
- **Product detail page** — everything described above (gallery, variations, reviews, etc.)
- **Cart** — list of items, totals, "Checkout" button
- **Checkout page** — form with address, payment method, order summary
- **Order tracking** — current status, transition timeline, items list
- **Profile** — personal info, order history, my reviews
- **Admin panel** — manage products, variations, categories, orders, stock
- **Profit / Loss page** (SuperAdmin only) — summary, charts, filters

---

## Acceptance Criteria

| What Must Work                                      |
|-----------------------------------------------------|
| ERD database diagram                                |
| JWT auth + roles (RBAC)                             |
| Catalog with filtering, sorting, and search         |
| Products with variations (SKU, price, stock, photos)|
| Product detail page (gallery, specs, etc.)          |
| Cart tied to variations                             |
| Checkout + stock deduction                          |
| Payment emulation                                   |
| Order statuses + transition history                 |
| Reviews & ratings                                   |
| Profit / loss                                       |
| Frontend — all pages functional                     |

---

## Tech Stack

- **Backend:** Go, `Ucode`
- **Frontend:** React or Next.js (your choice), deployed on **Vercel**
- **Database:** ERD required (dbdiagram.io / drawSQL / Mermaid)
- **Bonus:** Project Documentation / Profit Loss
