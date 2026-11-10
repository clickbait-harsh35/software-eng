# Student Attendance Management System (runnable starter)

This is a local PHP + MySQL implementation based on the uploaded project report's Chapter 12 schema and requirements. It provides:
- Login with ADMIN, TEACHER and STUDENT roles
- Password hashing, PHP sessions, prepared SQL statements and CSRF tokens
- Demo academic data (class, subjects, teacher allocations, student enrolments)
- Teacher manual attendance entry (Present / Absent)
- Student subject-wise attendance percentage and 75% shortage indicator
- Admin overview dashboard

**Not included yet:** full admin CRUD screens, QR-code generation/scanning, monthly charts/export, email/SMS notifications and production deployment. The report itself labels its code as a starter baseline and says these parts must be implemented and tested.

## Requirements
- Windows + XAMPP (Apache and MySQL)
- PHP 8.x with PDO MySQL enabled (included in standard XAMPP)
- A browser

## Run on Windows using XAMPP
1. Install XAMPP.
2. Open XAMPP Control Panel and click **Start** beside **Apache** and **MySQL**.
3. Copy the complete `student-attendance` folder into `C:\xampp\htdocs\`.
4. Open `http://localhost/phpmyadmin` in your browser.
5. Select the **Import** tab, choose `C:\xampp\htdocs\student-attendance\database\schema.sql`, and click **Import** / **Go**. This creates `attendance_db` and its tables.
6. Open `http://localhost/student-attendance/setup.php` once. You should see **Setup complete**. This creates fictional demo users and sample academic records.
7. Open `http://localhost/student-attendance/public/` and log in using one of the accounts below.
8. After setup is complete, delete `setup.php` from the project folder. It is only a one-time demo-data setup script.

## Demo login accounts
| Role | Username | Password |
|---|---|---|
| Administrator | `admin` | `Admin@123` |
| Teacher | `teacher1` | `Teacher@123` |
| Student | `student1` | `Student@123` |
| Student | `student2` | `Student@123` |

## How to test the workflow
1. Log in as `teacher1`.
2. Select a class/subject allocation and a date, then click **Load student list**.
3. Select Present or Absent for every student and click **Save attendance**.
4. Log out and log in as `student1` or `student2` to see the updated percentage.
5. Log in as `admin` to see the system overview.

## Database settings
The default XAMPP MySQL settings are in `config/config.php` (`root` with a blank password). If your MySQL root account has a password, update `DB_PASS` there.

## Important
- Use only fictional data in this demo.
- Change all demo passwords before any real use.
- This is an academic prototype, not a production-ready college system.
- QR attendance is described in the report but is not part of this runnable starter build.
