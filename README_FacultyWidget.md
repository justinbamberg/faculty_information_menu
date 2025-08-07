
# 📘 Faculty Dashboard Widget (D2L Brightspace)

This widget provides a central location for faculty to access tools, support links, and automated course-related processes inside D2L Brightspace. It's designed for use in a D2L **custom homepage widget** for instructors.

---

## ✅ Features Included

The widget contains collapsible `<details>` sections for:

1. **Faculty Training** – Links to instructional video tutorials (YouTube).
2. **D2L Webinars** – Scheduled Brightspace webinars with links and registration.
3. **Course Merge Request** – Info and form for merging multiple sections into one D2L course.
4. **Help Desk** – Contact form, email, and phone for support.
5. **Student Support System** – Referral form for counseling and TLC support.
6. **Attendance Tracking** – Link to Faculty Self-Service portal.
7. **Last Date of Attendance Info** – Policy and drop form for non-attending students.
8. **Submit Grades By** – Dynamically displays final grade due dates for enrolled courses.
9. **Add a ZZStudent (Demo Student)** – Launches tool for adding demo student to active courses.
10. **Create Sandbox Course** – Widget form to create a sandbox and enroll instructor + ZZStudent.

---

## 🧩 Intended Use

- Deployed as a **custom HTML widget** on the faculty D2L homepage.
- Responsive design using inline CSS (required by D2L to avoid being stripped).
- Allows instructors to access tools without navigating away from their homepage.

---

## 🔐 Permissions Checklist (for Admins)

Some functionality requires the following D2L permissions:

| Feature                         | Required Permissions                                                 |
|----------------------------------|----------------------------------------------------------------------|
| Create Sandbox Course            | `Course Creation`, `Enroll User`, `View My User Info`, `View Semesters` |
| Add ZZStudent                    | `Enroll User`, `View Course List`, `Create User` (if creating ZZStudent) |
| Submit Grades By                 | `View Enrollments`, `View Course Dates`, `Access CSV via Public API` |
| Access to API Apps               | Ensure appropriate **IP range + CSRF token** settings |
| View final grades due            | Must have API access to: `myenrollments`, custom CSV file (hosted on D2L) |

---

## 🔌 API Calls Used

### Submit Grades By Widget
- `GET /d2l/api/lp/1.51/users/whoami` – Get current user info
- `GET /d2l/api/lp/1.47/enrollments/myenrollments/` – Retrieve user's active course enrollments
- `GET /content/api-apps/important-dates/semester_dates.csv` – Pull due dates from hosted CSV

### Sandbox Course Creator
- `GET /d2l/api/lp/1.47/users/whoami` – Get instructor UserId
- `POST /d2l/api/lp/1.49/courses/` – Create new sandbox course
- `POST /d2l/api/lp/1.49/enrollments/` – Enroll instructor and student
- `GET /d2l/api/lp/1.45/users/?userName=` – Check if ZZStudent exists
- `POST /d2l/api/lp/1.45/users/` – Create new ZZStudent (if needed)

---

## ⚠️ Notes for Implementation

- D2L Brightspace widgets **require inline CSS**. Do not use `<style>` tags directly in the widget.
- If you need to use external CSS or JS, you must **host it in a separate folder** and link it via full URL.
- Avoid using script logic that requires external authentication unless running from an authenticated D2L session.

---

## 📷 Preview

A screenshot of the expanded widget layout is included as `widget-preview.png` in the full ZIP download.

---

## 🛠 Maintainer Notes

- All links and embedded tools should be updated each semester.
- Ensure instructors are not restricted by role when accessing merge forms or sandbox creators.
- The widget is safe to deploy to all faculty users, provided their roles have access to the required API scopes.

---

**Last Updated:** August 2025
