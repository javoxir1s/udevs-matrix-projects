# LMS (Learning Management System) — Exam Project

---

## Description

Develop a full-featured backend and frontend for an online learning platform where instructors create courses and students enroll, learn, and take assessments.

---

## Backend (Go)

### Authentication & Authorization
- JWT-based authentication (access token + refresh token)
- Role-based access control (RBAC)
- Roles:
    - SuperAdmin
    - Instructor
    - Student

### Courses
- Create / edit / delete courses (Instructor only)
- Course listing with filtering by category, difficulty level, and rating
- Course detail page (description, syllabus, instructor info)
- Publish / unpublish course

### Lessons
- Each course contains ordered lessons
- Lesson types: video (URL), text, file attachment
- Mark lesson as completed (Student)
- Progress tracking per student per course (e.g. 4/10 lessons completed)

### Enrollment
- Student enrolls in a course
- Enrollment statuses: `active` → `completed` → `dropped`
- Student can view their enrolled courses
- Instructor can view enrolled students

### Assessments (Tests)
- Instructor creates quizzes per course (multiple choice questions)
- Student takes the quiz and gets a score
- Pass / fail threshold set by instructor
- Store attempt history (score, date, time spent)

### Certificates
- Auto-generate certificate when student completes all lessons + passes final assessment
- Certificate contains: student name, course name, completion date, unique ID
- Verify certificate by unique ID (public endpoint)

### Profit / Loss
- Track course revenue (if paid courses): enrollment fee x number of students
- Instructor payout
- Filter by period (day / week / month)
- Status: **in profit** or **at a loss**
- Access restricted to `SuperAdmin` only

---

## Frontend (React / Next)

- Course catalog page with filters and search
- Course detail page with syllabus and enrollment button
- Student dashboard — enrolled courses, progress bars
- Lesson viewer page (video / text / file)
- Quiz page — take assessment, view results
- Instructor dashboard — manage courses, view enrolled students, create quizzes
- **Certificate** page — view and verify certificates
- **Profit / Loss** page (SuperAdmin only) — revenue summary

---

## Grading Criteria

| Criterion                              |
|----------------------------------------|
| Authentication + roles                 |
| Courses CRUD + filtering               |
| Lessons + progress tracking            |
| Enrollment management                  |
| Assessments (quizzes + scoring)        |
| Certificates (auto-generation + verify)|
| Profit / loss (summary + filtering)    |
| Frontend (all pages)                   |

---

## Tech Stack

- **Backend:** Go, `Ucode`
- **Frontend:** React / Next.js (choose one), deployed on **Vercel**
- **Bonus:** Project Documentation
