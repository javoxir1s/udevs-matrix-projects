# Real Estate — Technical Requirements

---

## From: Client
## To: Development Team

---

## What I Want

I need a real estate platform. Owners and agents list properties for sale or rent. Clients search, add to favorites, book viewings, and close deals. Rentals are managed with monthly payments. As the platform owner, I see the finances and control the process.

Not a bare-bones classifieds board — a full platform with viewings, deals, rental management, and analytics.

---

## Roles & Access

**SuperAdmin** — that's me, the platform owner. Full access: all properties, users, deals, finances. Role management.

**Agent** — lists properties, manages their listings, accepts/declines viewing requests, handles deals. Sees their own clients and stats.

**Owner** — lists their own properties, manages listings, confirms viewings. Can operate without an agent.

**Client** — buyer or tenant. Searches properties, adds to favorites, books viewings, closes deals, makes payments.

Authentication — JWT tokens (access + refresh). Passwords — bcrypt.

---

## Properties

An agent or owner creates a listing. Property data:
- Title (listing headline)
- Description (rich text)
- Property type: apartment / house / commercial / land
- Deal type: sale / rent
- Address, district / neighborhood
- Area (m²)
- Number of rooms
- Number of bathrooms
- Floor / total floors
- Year built
- Price, currency
- Photos (multiple, ordered, main photo separate)

**Amenities / features** — checkboxes:
- Parking, balcony, elevator, furniture, A/C, heating type, internet, pets allowed

**Variations / units** — if it's an apartment building or office center, one property can have multiple units. Each unit has its own area, floor, price, availability status.

Listing status: `active` → `reserved` → `sold` / `rented` → `archived`

Property catalog:
- Filtering by: type, price range (min–max), area range, number of rooms, district, deal type, amenities
- Sorting by: price, publication date, area
- Search by title or address
- Pagination

---

## Property Detail Page

When a client clicks on a property:

- **Photo gallery** — main photo + thumbnails, full-size viewing
- **Title, address, district, deal type badge** (sale / rent)
- **Price** — per month for rent, full amount for sale
- **Key specs** — area, rooms, bathrooms, floor, year built
- **Description** — rich text, detailed
- **Amenities list** — with icons (parking, balcony, elevator, etc.)
- **Map** — marker showing the property location
- **Agent / Owner info** — photo, name, rating, contacts
- **Similar / nearby listings** — recommendations
- **"Book a Viewing" button**
- **"Add to Favorites" button**
- **Agent reviews**

---

## Favorites

- Client adds properties to favorites with a single click (heart icon)
- View favorites list in the dashboard
- Remove from favorites

---

## Viewing Appointments

A client books a viewing for a property:
- Selects date and time (from the agent's/owner's available slots)
- Optionally adds a comment

Statuses: `pending` → `confirmed` → `completed` → `cancelled` → `no_show`

Agent / Owner confirms or declines the appointment.

Viewing history — visible to both the client and the agent.

Cancellation — with a reason.

---

## Deals

After a viewing, a deal is created (purchase or rental).

Deal data:
- Property
- Client
- Agent (if applicable)
- Deal type (purchase / rental)
- Amount
- Start date (for rentals)
- End date (for rentals)
- Terms (text)
- Contract file (attachment)

Deal statuses: `draft` → `pending_payment` → `completed` → `cancelled`

On deal completion — the property status changes to `sold` or `rented`.

The price is locked at the time of the deal (`price_at_deal`) — if the price changes tomorrow, the deal keeps the old price.

---

## Rental Management

If the deal is a rental, a rental agreement is created:
- Property, tenant, agent
- Start date, end date
- Monthly payment
- Deposit

Rental status: `active` → `expiring_soon` (30 days before end) → `expired` → `terminated`

Monthly payments are tracked:
- Payment date, amount, status (paid / overdue / pending)
- Monthly invoices auto-generated

Rental expiration notification.

---

## Payment

Emulation (no real gateway):
- For purchase: full amount or deposit
- For rental: monthly payments + initial deposit
- Statuses: `pending` → `paid` → `overdue` → `refunded`

---

## Reviews & Ratings

- Client leaves a review for the agent after a completed deal
- Rating 1–5 + text comment
- Average rating displayed in the agent's profile and on the property detail page

---

## Profit / Loss

SuperAdmin only.

- Revenue: platform commission per deal, commission from rentals
- Expenses: agent payouts, operational costs (simplified)
- Net profit / loss
- Filter by period: day, week, month, custom date range
- Clearly show: is the platform **in profit** or **at a loss**

---

## ERD (Database Diagram)

Before development starts — ERD diagram. All tables, relationships, data types. dbdiagram.io, drawSQL, or Mermaid. Include in documentation.

---

## Frontend — Pages I Need

- **Home page** — featured properties, popular districts, search bar
- **Catalog** — property cards, filters, search, sorting, list/map view toggle
- **Property detail page** — everything described above
- **Favorites** — saved listings
- **Viewing appointment form** — date/time selection
- **Client dashboard** — favorites, viewings, my deals, rental payments
- **Agent / Owner dashboard** — my properties, incoming viewing requests, deal management
- **Deal page** — create / manage deal with contract details
- **Rental management** — agreements, payment schedule, statuses
- **Profile** — personal info, reviews, settings
- **Profit / Loss page** (SuperAdmin only) — revenue, expenses, summary

---

## Acceptance Criteria

| What Must Work                                       |
|------------------------------------------------------|
| ERD database diagram                                 |
| JWT auth + roles (RBAC)                              |
| Properties (CRUD + filtering + search)               |
| Property detail page (gallery, map, etc.)            |
| Favorites                                            |
| Viewing appointments                                 |
| Deals (purchase / rental)                            |
| Rental management + monthly payments                 |
| Payment emulation                                    |
| Reviews & ratings                                    |
| Profit / loss                                        |
| Frontend — all pages functional                      |

---

## Tech Stack

- **Backend:** Go, `Ucode`
- **Frontend:** React or Next.js (your choice), deployed on **Vercel**
- **Database:** ERD required (dbdiagram.io / drawSQL / Mermaid)
- **Bonus:** Project Documentation, Profit / Loss, Cashflow
