# Real Estate — Exam Project

---

## Description

Develop a full-featured backend and frontend for a real estate platform with property listings, search, viewing appointments, deal management, and rental management.

---

## Backend (Go)

### Authentication & Authorization
- JWT-based authentication (access token + refresh token)
- Role-based access control (RBAC)
- Roles:
    - SuperAdmin
    - Agent
    - Owner
    - Client (buyer / tenant)

### Properties
- Create / edit / delete listing (Agent, Owner)
- Property type: apartment, house, commercial, land
- Deal type: sale / rent
- Property data: title, description, address, area (m²), number of rooms, floor, price, photos (multiple)
- Listing status: `active` → `reserved` → `sold` / `rented` → `archived`
- Property listing with filtering by: type, price, area, number of rooms, district, deal type
- Sorting by price, publication date, area
- Property detail page

### Favorites
- Client adds properties to favorites
- View favorites list

### Viewing Appointments
- Client books a viewing for a property
- Select date and time
- Statuses: `pending` → `confirmed` → `completed` → `cancelled`
- Agent / Owner confirms or declines the appointment
- Viewing history for client and agent

### Deals
- Create a deal after viewing (purchase or rental)
- Deal contains: property, client, agent, deal type, amount, date, terms
- Deal statuses: `draft` → `pending_payment` → `completed` → `cancelled`
- On deal completion — property status changes to `sold` / `rented`
- Save price at the time of deal (`price_at_deal`)

### Rental Management
- Manage rental agreements: start date, end date, monthly payment
- Rental status: `active` → `expiring_soon` → `expired` → `terminated`
- Track rental payments (monthly)
- Rental expiration notification (notification)

### Payment
- Emulated payment (no real gateway)
- For purchase: full amount or deposit
- For rental: monthly payments
- Statuses: `pending` → `paid` → `overdue` → `refunded`

### Ratings & Reviews
- Client leaves a rating (1–5) and review for the agent after a deal
- Average rating displayed in agent profile

### Profit / Loss
- Track revenue: platform commission per deal
- Track revenue from rentals
- Track expenses: agent payouts, operational costs (simplified)
- Net profit / loss calculation
- Filter by period (day / week / month)
- Status: **in profit** or **at a loss**
- Access restricted to `SuperAdmin` only

---

## Frontend (React / Next)

- Home page — property catalog with filters, search, and sorting
- Property detail page — photos, description, map, book viewing button
- Favorites page
- Viewing appointment form (select date and time)
- Client dashboard — favorites, viewing appointments, my deals, rental payments
- Agent / Owner dashboard — my properties, incoming viewing requests, deal management
- Deal page
- Rental management page — agreements, payments, statuses
- **Profit / Loss** page (SuperAdmin only) — revenue and expense summary

---

## Grading Criteria

| Criterion                              |
|----------------------------------------|
| Authentication + roles                 |
| Properties (CRUD + filtering)          |
| Favorites                              |
| Viewing appointments                   |
| Deals (purchase / rental)              |
| Rental management + payments           |
| Payment (emulation)                    |
| Ratings & reviews                      |
| Profit / loss (summary + filtering)    |
| Frontend (all pages)                   |

---

## Tech Stack

- **Backend:** Go, `Ucode`
- **Frontend:** React / Next.js (choose one), deployed on **Vercel**
- **Bonus:** Project Documentation
