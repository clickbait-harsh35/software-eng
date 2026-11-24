# Student Attendance Management System (SAMS)

Software Engineering project, Ramanujan College, University of Delhi (Semester 5, 2026-27).
PHP + MySQL web app that runs on XAMPP. Demo data is fictional.

## Requirements

- XAMPP (Apache and MySQL) on Windows
- A browser with JavaScript enabled

## Setup

### 1. Start XAMPP
Open the XAMPP Control Panel and start **Apache** and **MySQL**.

### 2. Copy the code
Copy the `student-attendance` folder into:

```
C:\xampp\htdocs\
```

If an older copy is there, replace it.

### 3. Set up the database
Open http://localhost/phpmyadmin and pick one option.

**Fresh install (easiest)**
1. If an old `attendance_db` exists and you want a clean start, drop it on the **Databases** tab.
2. Click the **Import** tab.
3. Choose `C:\xampp\htdocs\student-attendance\database\schema.sql` and click **Import**.

**Keep existing data (upgrade from v1)**
1. Click `attendance_db` in the left sidebar.
2. Click the **Import** tab.
3. Choose `database\migration_v2.sql` and click **Import**.
4. You should now see 13 tables, including `leave_requests`, `correction_requests` and `settings`.

If the import stops with "Duplicate entry" on the `ADD UNIQUE` line, the same class, subject and date was saved twice earlier. Open the `sessions` table, delete the duplicate row (the one with the higher `session_id`), delete its `attendance` rows first, then import again.

### 4. Load the demo data
Open http://localhost/student-attendance/setup.php once and wait for **Setup complete**.
Then **delete `setup.php`** from the folder.

Skip this step if you used the migration and your demo users already exist.

### 5. Log in
Go to http://localhost/student-attendance/public/

| Role    | Username   | Password     |
|---------|------------|--------------|
| Admin   | `admin`    | `Admin@123`  |
| Teacher | `teacher1` | `Teacher@123`|
| Student | `student1` | `Student@123`|
| Student | `student2` | see setup.php demo data |

Usernames and passwords are case-sensitive.

## Quick test

1. **teacher1:** Mark attendance, pick class and subject, load the list and save. Everyone defaults to Present; the dropdown also has Leave. Save the same date again to see the duplicate being blocked.
2. **student1:** Open the Leave tab and apply for leave. Check the dashboard and calendar.
3. **teacher1:** On Requests, approve the leave. Use Edit records to change a status (a reason is required).
4. **admin:** Open Audit log, Settings and Users.

## Features

- Roles: administrator, teacher, student (hashed passwords, CSRF tokens, 30-minute idle logout)
- Mark attendance as Present / Absent / Leave; duplicate sessions blocked
- Edit attendance within a set number of days, with a required reason and audit log
- Leave requests and approval; student correction requests
- Student dashboard, subject-wise percentage, month calendar, day-by-day view, profile
- Admin: users, classes, subjects, teacher allocations, enrolments, settings (default 75% threshold)
- Reports: class report and defaulter list, CSV export for Excel, print / save as PDF

## Not built yet (future scope)

- OTP sign-up and password reset
- E-mail / SMS notifications
- Backup and restore screen
- CAPTCHA and login lockout
- QR-code attendance

## Troubleshooting

- **"Database connection failed":** your MySQL root password is probably not blank. Set it as `DB_PASS` in `config/config.php`.
- **"Invalid username or password":** open the `users` table in phpMyAdmin. If it is empty, run `setup.php` (step 4). Also check that `is_active` is `1`.
- **setup.php says "Not Found":** it was deleted earlier. Copy it again from the zip into `C:\xampp\htdocs\student-attendance\`.
- **Pages error after upgrading:** the new tables are missing. Run `migration_v2.sql` (step 3).

## Notes

- The FACULTY table in the report is stored as `teachers` in the code, and login accounts for all roles are in `users`.
- Tables added in v2: `leave_requests`, `correction_requests`, `settings`.
- Delete `setup.php` after use, and change the demo passwords before any real use.
