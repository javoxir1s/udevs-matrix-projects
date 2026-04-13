# Food Delivery — Technical Requirements

---

## From: Client
## To: Development Team

---

## What I Want

I need a food delivery service. A customer opens the app, picks a restaurant, builds an order from the menu (with sizes, toppings), pays, and tracks the delivery. The restaurant accepts the order and cooks. The courier picks it up and delivers. As the platform owner, I see the finances and manage everything.

Not a simple restaurant directory — a full delivery service with dish variations, couriers, tracking, and analytics.

---

## Roles & Access

**SuperAdmin** — that's me, the platform owner. Full access: restaurants, orders, couriers, finances. Role management, manual courier assignment.

**Restaurant Owner** — manages their restaurant: profile, menu, dishes, variations. Accepts or rejects incoming orders. Sees their restaurant's stats. Cannot see platform finances.

**Courier** — sees available orders, accepts/declines, updates delivery status. Sees their profile and delivery history.

**Client** — browses restaurants, builds an order, pays, tracks delivery, leaves reviews.

Authentication — JWT tokens (access + refresh). Passwords — bcrypt.

---

## Restaurants

The owner registers their restaurant. Restaurant data:
- Name
- Description
- Address
- Cuisine category (Italian, Japanese, fast food, Uzbek, etc.)
- Logo
- Cover image
- Working hours (Monday–Sunday, open/close times)
- Minimum order amount
- Delivery fee

Restaurant listing supports:
- Filtering by: cuisine category, rating, price range, delivery time, status (open/closed — based on working hours)
- Search by name
- Sorting by: rating, delivery time, distance
- Pagination

---

## Restaurant Detail Page

When a customer clicks on a restaurant:

- **Cover image, logo, name, cuisine category**
- **Address, working hours, current status** (open / closed)
- **Average rating and review count**
- **Minimum order amount, delivery fee, estimated delivery time**
- **Menu** — grouped by categories (drinks, appetizers, mains, desserts). Each category is a separate section
- **Search within menu** — so you don't have to scroll through everything
- **Customer reviews** — list with rating, text, date
- **Map** — restaurant location

---

## Menu & Dishes

The restaurant owner manages the menu. Each dish:
- Name
- Description
- Category (drinks, appetizers, mains, desserts, etc.)
- Photo
- Base price
- Preparation time
- Availability (available / unavailable)

**Dish variations** — this is important. Example: "Margherita" pizza:
- Size: small (−20%), medium (base price), large (+30%)
- Spiciness: mild, medium, hot

Each variation has its own price modifier.

**Add-ons** — optional, separately priced:
- Extra cheese +15,000 sum
- Bacon +20,000 sum
- Jalapeños +5,000 sum

Menu filtering by: category, dietary tags (vegetarian, vegan, gluten-free).

---

## Dish Detail Page

When a customer clicks on a dish (modal or separate page):

- **Photo, name, description**
- **Base price + variation selector** (size, spiciness) — price updates in real time
- **Add-on list** with checkboxes and prices — price updates on selection
- **Preparation time**
- **Allergen info**
- **"Add to Cart" button** with quantity selector
- **Total price** (base + variation + add-ons) × quantity

---

## Cart

- Add / remove / change quantity and variations
- Cart is tied to one restaurant. If the customer adds a dish from another restaurant — warning: "Clear cart?"
- Displays: photo, name, variation, add-ons, unit price, quantity, line total
- Bottom: subtotal, delivery fee, grand total

---

## Order

- Place an order from the cart
- Specify: delivery address, phone number, comment, delivery time (ASAP / scheduled time)
- Save prices and variations at the time of order (`price_at_order`)
- Order statuses: `new` → `confirmed` → `preparing` → `ready` → `picked_up` → `delivered` → `cancelled`
- Each transition saved to history with timestamp
- Restaurant Owner confirms or rejects the order. If rejected — the customer gets a notification with the reason

---

## Couriers

Courier profile:
- Full name
- Phone
- Transport: walking / bicycle / car
- Photo

Courier status: `available` → `on_delivery` → `offline`

Courier assignment to order:
- Automatic — to the nearest available courier
- Manual — SuperAdmin assigns manually

Courier can accept or decline an order. If declined — the system finds the next one.

---

## Delivery Tracking

The customer sees:
- Current order status
- Transition history (timeline)
- Courier info: name, photo, phone, transport
- Estimated delivery time
- Notifications on status changes

---

## Payment

Emulation (no real gateway):
- Payment methods: cash to courier / online (card)
- Statuses: `pending` → `paid` → `failed` → `refunded`

---

## Reviews & Ratings

- Only after `delivered` status can the customer leave a review
- **Two separate ratings**: restaurant (food quality) and courier (delivery)
- Rating 1–5 + text comment
- Average rating displayed in the restaurant list and courier profile

---

## Profit / Loss

SuperAdmin only.

- Revenue: platform commission per order + delivery fee share
- Expenses: courier payouts, operational costs
- Net profit / loss
- Filter by period: day, week, month, custom date range
- Clearly show: is the platform **in profit** or **at a loss**

---

## ERD (Database Diagram)

Before development starts — ERD diagram. All tables, relationships, data types. dbdiagram.io, drawSQL, or Mermaid. Include in documentation.

---

## Frontend — Pages I Need

- **Home page** — restaurant list with filters, search, categories
- **Restaurant detail page** — everything described above
- **Dish detail modal / page** — variations, add-ons, live price
- **Cart** — items, subtotal, delivery fee, total
- **Checkout** — address, phone, payment method, delivery time
- **Order tracking** — status, timeline, courier info
- **Client dashboard** — order history, reviews, favorite restaurants
- **Restaurant Owner dashboard** — manage menu, dishes, variations, incoming orders
- **Courier dashboard** — available orders, accept/decline, update delivery status
- **Profit / Loss page** (SuperAdmin only) — revenue and expense summary

---

## Acceptance Criteria

| What Must Work                                       |
|------------------------------------------------------|
| ERD database diagram                                 |
| JWT auth + roles (RBAC)                              |
| Restaurants + detail page + filtering                |
| Menu + dish variations + add-ons                     |
| Dish detail page (variations, live price)            |
| Cart (single-restaurant scoped)                      |
| Order placement + statuses                           |
| Couriers + order assignment                          |
| Delivery tracking                                    |
| Payment emulation                                    |
| Reviews & ratings (restaurant + courier separately)  |
| Profit / loss                                        |
| Frontend — all pages functional                      |

---

## Tech Stack

- **Backend:** Go, `Ucode`
- **Frontend:** React or Next.js (your choice), deployed on **Vercel**
- **Database:** ERD required (dbdiagram.io / drawSQL / Mermaid)
- **Bonus:** Project Documentation
