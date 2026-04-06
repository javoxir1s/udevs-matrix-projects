# Food Delivery — Exam Project

---

## Description

Develop a full-featured backend and frontend for a food delivery service with a restaurant catalog, order placement, courier assignment, and real-time delivery tracking.

---

## Backend (Go)

### Authentication & Authorization
- JWT-based authentication (access token + refresh token)
- Role-based access control (RBAC)
- Roles:
    - SuperAdmin
    - Restaurant Owner
    - Courier
    - Client

### Restaurants
- Restaurant registration: name, address, cuisine category, photo, working hours
- Restaurant listing with filtering by cuisine category, rating, and status (open/closed)
- Restaurant detail page

### Menu
- Restaurant Owner creates / edits / deletes dishes
- Dish: name, description, price, photo, category (drinks, mains, desserts, etc.)
- Mark dish as available / unavailable
- Filter menu by category

### Cart
- Add / remove / update dish quantity
- Cart is tied to one restaurant (warning when adding from another)
- View cart with total amount + delivery fee

### Order
- Place an order from the cart
- Specify delivery address and comment
- Save dish prices at the time of order (`price_at_order`)
- Order statuses: `new` → `confirmed` → `preparing` → `ready` → `picked_up` → `delivered` → `cancelled`
- Save each transition to history with timestamp
- Restaurant confirms / rejects the order

### Couriers
- Courier profile: name, phone, transport (walking / bicycle / car)
- Courier status: `available` → `on_delivery` → `offline`
- Assign courier to order (manually by SuperAdmin or auto-assign to available courier)
- Courier can accept / decline an order

### Delivery Tracking
- Client sees current order status and transition history
- Display assigned courier info (name, phone)
- Notifications on status change (notification)

### Payment
- Emulated payment (no real gateway)
- Payment methods: cash to courier / online
- Statuses: `pending` → `paid` → `failed` → `refunded`

### Ratings & Reviews
- Client leaves a rating (1–5) and review after delivery
- Restaurant rating and courier rating — separate
- Average rating displayed in restaurant list and courier profile

### Profit / Loss
- Track revenue: platform commission per order + delivery fee
- Track expenses: courier payouts
- Net profit / loss calculation
- Filter by period (day / week / month)
- Status: **in profit** or **at a loss**
- Access restricted to `SuperAdmin` only

---

## Frontend (React / Next)

- Home page — restaurant list with filters and search
- Restaurant page — menu with categories
- Cart with total calculation and delivery fee
- Checkout form (address, comment, payment method)
- **Order tracking** page — current status, history, courier info
- Client dashboard — order history, reviews
- Restaurant Owner dashboard — manage menu, incoming orders, confirm/reject
- Courier dashboard — available orders, accept/decline, update delivery status
- **Profit / Loss** page (SuperAdmin only) — revenue and expense summary

---

## Grading Criteria

| Criterion                              |
|----------------------------------------|
| Authentication + roles                 |
| Restaurants + menu (CRUD)              |
| Cart                                   |
| Order placement + statuses             |
| Couriers + order assignment            |
| Delivery tracking                      |
| Payment (emulation)                    |
| Ratings & reviews                      |
| Profit / loss (summary + filtering)    |
| Frontend (all pages)                   |

---

## Tech Stack

- **Backend:** Go, `Ucode`
- **Frontend:** React / Next.js (choose one), deployed on **Vercel**
- **Bonus:** Project Documentation
