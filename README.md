# DEMI PENSION BENAYAD KHLIFA 200 R

A design and development starting guide for using **Claude** and **Claude Code** to build a clean, reliable, and practical demi-pension management experience.

This README is written as the project entry point. Put it in the root of the project before opening the folder with Claude Code.

---

## 1. Project Purpose

The goal is to design a complete, professional system for managing a **demi-pension / half-board service** for **Benayad Khlifa 200 R**.

The final product should help the team manage daily operations with less confusion, fewer manual mistakes, and a clear view of students, subscriptions, payments, meals, attendance, and reports.

### Main Objectives

- Make registration and subscription management simple.
- Track students who are subscribed to demi-pension.
- Track payments, unpaid balances, refunds, and payment history.
- Manage daily meal attendance or meal access.
- Provide clear dashboards for administrators and staff.
- Generate useful reports for accounting, control, and planning.
- Keep the interface simple enough for non-technical users.
- Build a design that can later become a real web/mobile application.

---

## 2. Intended Users

Design the system around these users first:

### 2.1 Administrator

Responsible for global management.

Needs:
- Overview dashboard.
- Student and subscription management.
- Staff/user management.
- Reports and exports.
- Settings and school-year configuration.

### 2.2 Finance / Cashier User

Responsible for payments and financial tracking.

Needs:
- Add payments quickly.
- See paid, partially paid, and unpaid students.
- Print or export receipts.
- Filter by date, class/group, subscription type, or payment status.

### 2.3 Canteen / Control Staff

Responsible for daily meal access and attendance.

Needs:
- Fast student search.
- Simple check-in/check-out or meal validation.
- Clear status: allowed, not allowed, already served, unpaid, absent, suspended.
- Minimal clicks during busy hours.

### 2.4 Parent / Student View, Optional Later

Only add this if needed after the internal system is stable.

Possible needs:
- View subscription status.
- View payment status.
- View menu or announcements.
- Download receipt.

---

## 3. Core Product Scope

Claude and Claude Code should start with a focused MVP before adding advanced features.

### MVP Features

1. **Dashboard**
   - Total subscribed students.
   - Paid / unpaid / partially paid counts.
   - Today’s expected meals.
   - Today’s served meals.
   - Alerts: unpaid students, missing records, expiring subscriptions.

2. **Students**
   - Add/edit student.
   - Search student by name, ID, class, group, or guardian.
   - Student profile page.
   - Student status: active, inactive, suspended, transferred.

3. **Subscriptions**
   - Create demi-pension subscription.
   - Define period: month, trimester, semester, year, or custom date range.
   - Track active, expired, cancelled, suspended subscriptions.
   - Link subscription to payment status.

4. **Payments**
   - Record payment.
   - Support full and partial payments.
   - Payment receipt reference.
   - Payment history by student.
   - Balance due.
   - Export payment list.

5. **Daily Meal Attendance / Access Control**
   - Validate if a student can eat today.
   - Mark student as served.
   - Prevent duplicate serving.
   - Show reason if blocked: unpaid, inactive, already served, subscription expired.

6. **Reports**
   - Daily attendance report.
   - Monthly payment report.
   - Unpaid students report.
   - Subscribed students report.
   - Export to CSV/PDF later.

7. **Settings**
   - Academic year.
   - Meal price or subscription price.
   - Classes/groups.
   - User roles.
   - School/service information.

---

## 4. Design Principles

The design should be practical, fast, and easy to understand.

### 4.1 Simplicity First

Every screen should answer one question clearly:

- Who is subscribed?
- Who paid?
- Who did not pay?
- Who can eat today?
- What happened today?

Avoid decorative complexity. This is an operational system, not a marketing website.

### 4.2 Fast Daily Workflow

The canteen/control flow must be extremely fast:

1. Search or scan student.
2. See status immediately.
3. Validate meal with one action.
4. Move to the next student.

### 4.3 Clear Status Colors and Labels

Use consistent labels everywhere:

- **Active**
- **Expired**
- **Paid**
- **Partially Paid**
- **Unpaid**
- **Suspended**
- **Served Today**
- **Not Served**
- **Blocked**

Do not use only colors. Always include readable text or icons for accessibility.

### 4.4 Mobile-Friendly, Desktop-Ready

The system should work well on:

- Office desktop/laptop.
- Tablet at the canteen entrance.
- Mobile phone for quick checks.

Design mobile-first, then improve for desktop tables and dashboards.

### 4.5 Bilingual-Ready

Prepare the interface so it can support:

- French labels.
- Arabic labels if needed.
- English technical naming internally.

Do not hard-code visible labels directly in components if the project becomes multilingual.

---

## 5. Recommended Information Architecture

Suggested main navigation:

```text
Dashboard
Students
Subscriptions
Payments
Meal Control
Reports
Settings
```

### Suggested Page Structure

```text
/dashboard
/students
/students/new
/students/:id
/subscriptions
/subscriptions/new
/payments
/payments/new
/meal-control
/reports
/settings
```

---

## 6. Recommended Data Model

Claude Code should not blindly implement the database until requirements are confirmed, but this is the starting model.

### Student

```text
id
student_number
first_name
last_name
date_of_birth
class_name
group_name
guardian_name
guardian_phone
status
created_at
updated_at
```

### Subscription

```text
id
student_id
subscription_type
start_date
end_date
total_amount
status
notes
created_at
updated_at
```

### Payment

```text
id
student_id
subscription_id
amount_paid
payment_method
payment_date
receipt_number
created_by
notes
created_at
```

### MealAttendance

```text
id
student_id
subscription_id
meal_date
meal_type
status
validated_by
validated_at
notes
```

### User

```text
id
full_name
email
role
status
created_at
updated_at
```

### AuditLog

```text
id
user_id
action
entity_type
entity_id
old_value
new_value
created_at
```

---

## 7. Design System Direction

### Visual Style

Use a clean administrative design:

- Light background.
- Clear cards.
- Large readable tables.
- Strong search and filter controls.
- Clear empty states.
- Minimal decoration.
- Professional school/service feeling.

### Suggested UI Components

- App shell / sidebar.
- Top bar with current academic year and user menu.
- Dashboard stat cards.
- Data tables with filters.
- Student profile card.
- Status badges.
- Payment summary card.
- Meal validation panel.
- Confirmation dialogs.
- Toast notifications.
- Export buttons.
- Empty states.
- Error states.

### Accessibility Rules

- Text must be readable on mobile and desktop.
- Do not rely on color alone.
- Buttons must have clear labels.
- Tables should have clear column names.
- Forms should show validation messages.
- Important actions should ask for confirmation.

---

## 8. Suggested Technical Direction

Use this only if the project does not already have a defined stack.

### Recommended Stack

- **Frontend:** Next.js + TypeScript
- **Styling:** Tailwind CSS
- **UI Components:** shadcn/ui or a similar accessible component system
- **Database:** PostgreSQL
- **Backend:** Next.js API routes, NestJS, Laravel, or another clear backend framework
- **Authentication:** Role-based access control
- **Exports:** CSV first, PDF later

### Important

If an existing stack already exists in the source files, Claude Code must follow the existing stack instead of replacing it.

---

## 9. Claude / Claude Code Workflow

Claude Code is useful because it can inspect the project, edit files, run commands, and work inside the terminal or IDE. Use it as a careful assistant, not as an uncontrolled automatic generator.

### Step 1 — Source Discovery

Ask Claude Code:

```text
Read the entire project structure. Summarize what files exist, what the current stack is, what is missing, and what decisions we need before designing the demi-pension system. Do not edit files yet.
```

Claude Code should identify:

- Existing framework.
- Existing routes/pages.
- Existing components.
- Existing assets.
- Existing design style.
- Missing requirements.
- Possible risks.

### Step 2 — Product Requirements

Ask:

```text
Using README.md as the source of truth, create a clear product requirements document for the demi-pension system. Separate MVP features from later features. Ask only the most important unresolved questions.
```

### Step 3 — Design Map

Ask:

```text
Create the full app information architecture, user flows, and screen list for the demi-pension system. Focus on the fastest workflow for student registration, payment tracking, and daily meal validation.
```

### Step 4 — Wireframe Before Code

Ask:

```text
Create low-fidelity wireframes in text for each MVP screen before writing code. For every screen, describe the layout, main actions, table columns, empty states, and error states.
```

### Step 5 — Component Plan

Ask:

```text
Create a reusable component plan for this app. Include layout components, cards, tables, forms, status badges, dialogs, and meal validation components. Do not code yet.
```

### Step 6 — Implement Incrementally

Build one part at a time:

1. App shell and navigation.
2. Dashboard layout.
3. Students list and student profile.
4. Subscription screens.
5. Payment screens.
6. Meal control screen.
7. Reports.
8. Settings.

Do not ask Claude Code to build everything in one huge step.

### Step 7 — Review and Refine

After each implementation step, ask:

```text
Review the changes for usability, consistency, accessibility, bugs, and missing edge cases. Suggest improvements before we continue.
```

---

## 10. Claude Code Guardrails

Claude Code must follow these rules:

1. Do not delete existing source files unless explicitly asked.
2. Do not replace the existing tech stack without explaining why.
3. Do not make database migrations without a clear schema plan.
4. Do not hard-code fake business rules as final logic.
5. Do not expose private data, secrets, API keys, or credentials.
6. Do not create huge files when smaller reusable components are better.
7. Do not ignore mobile layout.
8. Do not use vague labels like “Item” or “Data”; use real product language.
9. Always keep user roles in mind.
10. Always explain what changed after editing files.

---

## 11. First Claude Code Command Prompt

Use this as the first prompt after opening the project folder:

```text
You are helping design and build the DEMI PENSION BENAYAD KHLIFA 200 R system.

First, read README.md and inspect the project structure. Do not edit files yet.

Return:
1. Current project stack and structure.
2. Existing files that matter for the design.
3. Missing files or missing requirements.
4. Recommended first design plan.
5. Risks or unclear decisions.
6. A step-by-step implementation plan for the MVP.

Important rules:
- Follow the existing stack if one exists.
- Keep the UI simple, fast, and operational.
- Prioritize students, subscriptions, payments, and daily meal control.
- Do not make destructive changes.
```

---

## 12. Suggested `CLAUDE.md` Content

Create a `CLAUDE.md` file later with this content so Claude Code always remembers the project rules:

```markdown
# Claude Instructions for DEMI PENSION BENAYAD KHLIFA 200 R

This project is a demi-pension / half-board management system.

Priorities:
1. Simple operational UI.
2. Fast student search and daily meal validation.
3. Clear payment/subscription status.
4. Mobile-friendly and desktop-ready layout.
5. Reusable components.
6. Safe, incremental changes.

Never:
- Delete files without permission.
- Replace the stack without justification.
- Hide important payment or subscription status.
- Rely on color only for statuses.
- Build huge all-in-one components.

Always:
- Read README.md first.
- Summarize the plan before editing.
- Make small changes.
- Explain what changed.
- Check edge cases.
```

---

## 13. Design Acceptance Checklist

Before accepting the design, verify:

### Dashboard

- [ ] Shows important totals clearly.
- [ ] Shows payment and subscription alerts.
- [ ] Shows today’s meal status.

### Students

- [ ] Search is fast and obvious.
- [ ] Student profile is complete.
- [ ] Status is clear.

### Subscriptions

- [ ] Start/end dates are clear.
- [ ] Expired subscriptions are obvious.
- [ ] Subscription status matches payment situation.

### Payments

- [ ] Partial payments are supported.
- [ ] Balance due is clear.
- [ ] Receipt/reference is visible.
- [ ] Payment history is easy to understand.

### Meal Control

- [ ] Staff can validate a student quickly.
- [ ] Duplicate meals are blocked.
- [ ] Block reasons are clear.
- [ ] Works well on tablet/mobile.

### Reports

- [ ] Daily report exists.
- [ ] Monthly payment report exists.
- [ ] Unpaid students report exists.
- [ ] Export is planned or implemented.

### General UI

- [ ] Mobile-friendly.
- [ ] Clear labels.
- [ ] Accessible status indicators.
- [ ] No confusing navigation.
- [ ] No unnecessary decoration.

---

## 14. Later Features

Add these only after the MVP is stable:

- QR code or barcode student cards.
- Parent/student portal.
- SMS or WhatsApp payment reminders.
- PDF receipt generation.
- Menu planning.
- Stock/ingredient management.
- Multi-school support.
- Advanced accounting exports.
- Offline mode for meal control.
- Biometric or card-based access control, if legally and practically appropriate.

---

## 15. Important Open Questions

These should be answered before final implementation:

1. What does “200 R” specifically represent in this project?
2. Is the system for one school/service only or multiple locations?
3. What languages must the final UI support?
4. What is the exact subscription pricing model?
5. Are payments monthly, trimester-based, yearly, or flexible?
6. Are partial payments allowed?
7. Does each student have a unique ID/card number?
8. Will meal validation use manual search, QR code, barcode, or card scan?
9. Who can edit or delete payments?
10. What reports are legally or administratively required?

---

## 16. Recommended Next Step

Start with design, not code.

The correct first milestone is:

```text
A complete MVP screen map + wireframes + data model + component plan.
```

Only after that should Claude Code begin implementing files.
