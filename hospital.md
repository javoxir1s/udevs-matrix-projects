# Hospital / Clinic Management — Exam Project

---

## Description

Develop a full-featured backend and frontend for a hospital/clinic management system that handles patient registration, doctor scheduling, appointments, medical records, and billing.

---

## Backend (Go)

### Authentication & Authorization
- JWT-based authentication (access token + refresh token)
- Role-based access control (RBAC)
- Roles:
    - SuperAdmin
    - Doctor
    - Receptionist
    - Patient

### Doctors
- Doctor profile: name, specialization, experience, photo
- Doctor listing with filtering by specialization and availability
- Doctor schedule management (working days, time slots)

### Patients
- Patient registration with personal info
- Patient profile: name, age, gender, blood type, allergies, contact info
- Patient search (by name, phone, or ID)

### Appointments
- Patient books an appointment with a doctor
- Choose available time slot from doctor's schedule
- Appointment statuses: `scheduled` → `in_progress` → `completed` → `cancelled`
- Only available slots are shown (no double-booking)
- Receptionist can manage appointments for walk-in patients
- Send appointment reminder (notification)

### Medical Records
- Doctor creates a medical record after appointment
- Record contains: diagnosis, symptoms, prescription, notes, date
- Each patient has a full medical history (list of all records)
- Only the assigned Doctor and the Patient can view the record
- SuperAdmin has read access to all records

### Prescriptions
- Doctor issues a prescription as part of a medical record
- Prescription contains: medication name, dosage, frequency, duration
- Patient can view their active prescriptions

### Billing
- Auto-generate invoice after appointment is completed
- Invoice contains: consultation fee, any additional charges, total
- Payment statuses: `unpaid` → `paid` → `refunded`
- Emulated payment (no real gateway)

### Profit / Loss
- Track revenue from paid invoices
- Track expenses (doctor salaries — simplified, fixed monthly amount)
- Net profit / loss calculation
- Filter by period (day / week / month)
- Status: **in profit** or **at a loss**
- Access restricted to `SuperAdmin` only

---

## Frontend (React / Next)

- Doctor listing page with filters by specialization
- Doctor profile page with schedule and booking form
- Patient dashboard — upcoming appointments, medical history, prescriptions
- Appointment booking page — select doctor, date, time slot
- Doctor dashboard — today's appointments, patient records, create medical record
- Receptionist dashboard — manage appointments, register walk-in patients
- Medical record view page
- Invoice / billing page with payment status
- **Profit / Loss** page (SuperAdmin only) — revenue and expense summary

---

## Grading Criteria

| Criterion                              |
|----------------------------------------|
| Authentication + roles                 |
| Doctors + schedule management          |
| Patient registration + search          |
| Appointment booking (no double-booking)|
| Medical records + history              |
| Prescriptions                          |
| Billing + payment emulation            |
| Profit / loss (summary + filtering)    |
| Frontend (all pages)                   |

---

## Tech Stack

- **Backend:** Go, `Ucode`
- **Frontend:** React / Next.js (choose one), deployed on **Vercel**
- **Bonus:** Project Documentation
