# KSU Procurement Requisition System

Digital procurement requisition system for Kaduna State University (KSU), built as a final-year project case study.

## Stage 1 — Foundation + Authentication (this delivery)

This is the first of several staged deliveries. It includes:

- Project scaffold (Next.js 14.2.3 App Router, all locked dependencies in `package.json`)
- Full constants: 7 roles, all 8 KASU colleges with faculties/departments and routing types, requisition categories/urgency/status options
- Mongoose models: `User`, `Requisition`, `Approval`, `AuditLog`
- Core lib: MongoDB connection, JWT auth (24h expiry) + bcrypt, Nodemailer email templates for every status transition, Cloudinary upload helper, PDFKit requisition export, and the approval **routing engine** (`lib/routing.js`) that builds the correct approval chain per college — including the special Postgraduate and Basic Studies paths — and flags requisitions above ₦10,000,000 for escalation
- Joi validators (relaxed for drafts, strict for submission)
- Full auth flow: self-registration (role + college/faculty/department picker, goes to "pending" for admin approval), admin registration (self-locks once 2 admins exist), login, logout, forgot/reset password (email-based)
- Route protection middleware (edge-compatible via `jose`)
- Shared UI primitives: `Button`, `InputField`, `SelectField`, `CollegeFacultyDeptSelect`

## Not yet included (future stages)

- Dashboard (role-based views for all 7 roles)
- Requisitions module (3-step wizard, list, detail, drafts, edit/resubmit)
- Approvals queue (approve / return / reject)
- Admin user management (invite, approve pending, edit, deactivate)
- Reports & Analytics, Audit Trail views
- Settings page
- Sidebar/Navbar layout for authenticated pages

## Setup

1. `npm install`
2. Copy `.env.example` to `.env.local` and fill in real values (MongoDB Atlas URI, JWT secret, SMTP credentials, Cloudinary credentials)
3. Since there's no seed script, create your first administrator account by visiting `/register-admin` after running the app — this route is only available while fewer than 2 admin accounts exist
4. `npm run dev`

## Notes

- No seed script anywhere in this project, by design.
- Admin accounts are hard-capped at exactly 2.
- The system's scope ends at requisition approval — there is no vendor directory, purchase order, or budget/bursary module.
