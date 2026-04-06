# E-Commerce — Exam Project

---

## Description

Develop a full-featured backend and frontend for an online store with product purchasing and order status tracking functionality.

---

## Backend (Go)

### Authentication & Authorization
- JWT-based authentication (access token + refresh token)
- Role-based access control (RBAC)
- Roles:
    - SuperAdmin
    - Content Manager
    - WareHouse Admin
    - Client

### Catalog
- Product listing with filtering by category and price
- Product detail page
- Stock quantity tracking (`stock_qty`)

### Cart
- Add / remove / update product quantity
- View cart with total amount

### Order
- Place an order from the cart
- On checkout — deduct `stock_qty`
- If insufficient stock — return an error
- Save the product price at the time of order (`price_at_order`)

### Payment
- Emulate payment (no real payment gateway)
- Statuses: `pending` → `paid` → `failed`

### Order Status
- Lifecycle: `new` → `paid` → `processing` → `shipped` → `delivered`
- Save each transition to history with timestamp and comment
- Only `admin` can change the status

### Profit / Loss

- Filter by period (day / week / month)
- Status: **in profit** or **at a loss**
- Access restricted to `SuperAdmin` only

---

## Frontend (React / Next)

- Catalog page with product cards
- Cart with total calculation
- Checkout form
- **Order tracking** page — displays current status and transition history
- **Profit / Loss** page (SuperAdmin only) — summary of revenue, costs, and net profit

---

## Grading Criteria

| Criterion                              |
|----------------------------------------|
| Authentication + roles                 |
| Catalog + filtering                    |
| Cart                                   |
| Checkout + stock deduction             |
| Payment (emulation)                    |
| Status transitions + history           |
| Profit / loss (summary + filtering)    |
| Frontend (all pages)                   |

---

## Tech Stack

- **Backend:** Go, `Ucode`
- **Frontend:** React / Next.js (choose one), deployed on **Vercel**
- **Bonus:** Project Documentation
