# Hospital / Clinic Management — Technical Requirements

---

## From: Client
## To: Development Team

---

## What I Want

I need a clinic management system. A patient visits the website, picks a doctor, books an appointment, comes in, gets a diagnosis and prescription — and all of this is recorded in the system. The doctor sees patients and fills out medical records. The receptionist manages the schedule. As the owner, I see the finances and control the process.

Not a "notebook" — a full-fledged system with scheduling, medical records, prescriptions, billing, and analytics.

---

## Roles & Access

**SuperAdmin** — that's me, the clinic owner. Full access: all doctors, patients, appointments, medical records (read-only), finances. User role management.

**Doctor** — sees patients. Views their appointments for today and upcoming ones. Creates medical records and prescriptions. Can only see medical records of their own patients. Manages their own schedule.

**Receptionist** — registers new patients, manages appointments (create, confirm, cancel), books walk-in patients. Cannot see medical records or finances.

**Patient** — registers, picks a doctor, books an appointment, views their medical records, prescriptions, and invoices.

Authentication — JWT tokens (access + refresh). Passwords — bcrypt.

---

## Doctors

Doctor profile contains:
- Full name
- Specialization (general practitioner, cardiologist, neurologist, dentist, etc.)
- Years of experience
- Photo
- Bio
- Consultation fee
- Languages

Doctor listing supports:
- Filtering by: specialization, rating, availability, price range
- Search by name
- Pagination

Doctor schedule — configurable:
- Working days of the week
- Time intervals (e.g.: 09:00–12:00, 14:00–18:00)
- Single slot duration (e.g. 30 minutes)
- The system automatically generates available slots based on the schedule

---

## Doctor Detail Page

When a patient clicks on a doctor, they land here:

- **Photo, full name, specialization, years of experience**
- **Bio** — detailed info about the doctor, education, achievements
- **Languages**
- **Consultation fee**
- **Average rating and review count**
- **Schedule** — weekly calendar view, showing when the doctor works
- **Available slots** — for the next 7 days, only free slots. Booked ones are hidden
- **Patient reviews** — list of reviews with rating, name, date, text
- **"Book Appointment" button**

---

## Patients

Patient registration — detailed form:
- Full name
- Date of birth
- Gender
- Blood type
- Allergies (list)
- Chronic conditions
- Emergency contact (name, phone, relationship)
- Home address
- Phone, email

Patient search (for Receptionist, Doctor, SuperAdmin): by name, phone, or patient ID.

---

## Appointments

A patient books an appointment with a doctor:
- Selects a doctor
- Selects a date
- Sees only available slots (booked ones are hidden)
- Specifies reason for visit and a comment

Appointment data: doctor, patient, date, time, reason for visit, comment.

Statuses: `scheduled` → `confirmed` → `in_progress` → `completed` → `cancelled` → `no_show`

Important: **no double-booking**. If two patients try to book the same slot simultaneously — only one gets it. This must be enforced at the database transaction level.

The receptionist can book walk-in patients — to the nearest available slot.

Cancellation — with a reason.

Appointment reminder — notification.

---

## Medical Records

After completing an appointment, the doctor creates a medical record:
- Diagnosis
- Symptoms
- Examination notes
- Prescription (linked to the record)
- Lab results — attached files (PDF, photos)
- Date

Each patient has a complete medical history — a chronological list of all medical records.

Medical record access:
- Treating doctor — full access
- Patient — read-only for their own records
- SuperAdmin — read-only for all records
- Receptionist — **cannot see** medical records

---

## Prescriptions

The doctor issues a prescription as part of a medical record. A prescription contains a list of medications:
- Medication name
- Dosage (e.g. "500 mg")
- Frequency (e.g. "3 times a day")
- Duration (e.g. "7 days")
- Instructions (e.g. "after meals, with water")

A prescription has an issue date and an expiration date.

The patient can view their active and past prescriptions.

---

## Billing

After an appointment is completed (`completed` status), an invoice is auto-generated:
- Consultation fee
- Additional services (lab tests, procedures) — as separate line items
- Total amount
- Issue date

Payment statuses: `unpaid` → `paid` → `refunded`

Payment — emulated (no real gateway).

---

## Reviews & Ratings

- A patient can only leave a review after a completed appointment (`completed`)
- Rating 1–5 and text comment
- Average rating displayed in the doctor's profile and in the doctor listing

---

## Profit / Loss

SuperAdmin only.

- Revenue: paid invoices
- Expenses: doctor salaries (simplified — fixed monthly amount), operational costs
- Net profit / loss
- Filter by period: day, week, month, custom date range
- Clearly show: is the clinic **in profit** or **at a loss**

---

## ERD (Database Diagram)

Before development starts — ERD diagram. All tables, relationships, data types. dbdiagram.io, drawSQL, or Mermaid. Include in documentation.

---

## Frontend — Pages I Need

- **Home page** — doctor search, featured specializations, banners
- **Doctor listing** — cards, filters (specialization, rating, price), search
- **Doctor detail page** — everything described above
- **Appointment booking** — date, slot, reason selection
- **Patient dashboard** — upcoming appointments, medical history, prescriptions, invoices
- **Doctor dashboard** — today's appointments, patient list, create medical record and prescription
- **Receptionist dashboard** — manage appointments, register walk-in patients
- **Medical record view** — diagnosis, notes, lab results, prescription
- **Invoice page** — payment status, details
- **Profile** — personal info, settings
- **Profit / Loss page** (SuperAdmin only) — revenue, expenses, summary

---

## Acceptance Criteria

| What Must Work                                       |
|------------------------------------------------------|
| ERD database diagram                                 |
| JWT auth + roles (RBAC)                              |
| Doctors + detail page + schedule                     |
| Patient registration + search                        |
| Appointment booking (no double-booking)              |
| Medical records + history                            |
| Prescriptions with medications                       |
| Billing + payment emulation                          |
| Reviews & ratings                                    |
| Profit / loss                                        |
| Frontend — all pages functional                      |

---

## Tech Stack

- **Backend:** Go, `Ucode`
- **Frontend:** React or Next.js (your choice), deployed on **Vercel**
- **Database:** ERD required (dbdiagram.io / drawSQL / Mermaid)
- **Bonus:** Project Documentation, Profit / Loss, Cashflow
