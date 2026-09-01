<div align="center">

# 🎓 Student ERP Management System

[![Django Version](https://img.shields.io/badge/Django-4.2.24-092E20?style=for-the-badge&logo=django&logoColor=white)](https://www.djangoproject.com/)
[![Python Version](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Database](https://img.shields.io/badge/Database-SQLite%20%7C%20PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Frontend](https://img.shields.io/badge/Frontend-HTML5%20%7C%20CSS3%20%7C%20JS-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

<br>

**A modern, production-ready, role-based academic management ecosystem built on Django.**  
*Streamlining administration, faculty workflows, and student life under a single unified architecture.*

<br>

[Explore Features](#-role-based-features) • [Quick Start](#-quick-start-guide) • [Architecture](#-system-architecture) • [Roadmap](#-future-roadmap)

---

</div>

<br>

## 📌 Executive Summary

The **Student ERP Management System** solves administrative fragmentation in academic institutions by consolidating records, communication channels, financial logging, and evaluation metrics into a single multi-tenant workspace.

### Core User Roles

| Role | Access Level | Primary Scope |
| :--- | :--- | :--- |
| 👨‍💼 **HOD / Admin** | **Full System Access** | Academic sessions, staff & student registry, leaves, global alerts, fee structures |
| 👨‍🏫 **Staff / Faculty** | **Restricted / Operational** | Subject management, attendance grading, internal tests, leave dispatch |
| 🎓 **Student** | **Self-Service** | Attendance tracking, grade-sheet inspection, fee receipts, leave requests |

---

## 🏗️ System Architecture

```text
                                  ┌────────────────────────────────┐
                                  │   Student ERP Web Platform    │
                                  └───────────────┬────────────────┘
                                                  │
                 ┌────────────────────────────────┼────────────────────────────────┐
                 ▼                                ▼                                ▼
      ┌────────────────────┐            ┌────────────────────┐           ┌────────────────────┐
      │  HOD / Admin View  │            │     Staff View     │           │    Student View    │
      └──────────┬─────────┘            └──────────┬─────────┘           └──────────┬─────────┘
                 │                                 │                                │
                 └────────────────────────────────┼────────────────────────────────┘
                                                  ▼
                                 ┌───────────────────────────────────┐
                                 │   Custom Role/Auth Middleware     │
                                 └────────────────┬──────────────────┘
                                                  ▼
                                 ┌───────────────────────────────────┐
                                 │       Django 4.2 Application      │
                                 │  (Views, ORM Models, Form Engine) │
                                 └────────────────┬──────────────────┘
                                                  ▼
                         ┌────────────────────────┴────────────────────────┐
                         ▼                                                 ▼
             ┌───────────────────────┐                         ┌───────────────────────┐
             │ SQLite / PostgreSQL   │                         │ SMTP / Static Storage │
             └───────────────────────┘                         └───────────────────────┘
```

---

## ⚡ Role-Based Permissions Matrix

| Functional Module | 👨‍💼 HOD / Admin | 👨‍🏫 Staff | 🎓 Student |
| :--- | :---: | :---: | :---: |
| **User & Role Provisioning** | Full CRUD | ❌ | ❌ |
| **Course & Session Setup** | Full CRUD | ❌ | ❌ |
| **Daily Attendance** | View / Audit | Mark / Edit | View Personal |
| **Exam & Result Entry** | View All | Enter / Edit | View Personal |
| **Fee Structuring & Invoicing** | Manage & Remind | ❌ | View & Download |
| **Leave Management** | Review / Decide | Apply & Track | Apply & Track |
| **Campus Notifications** | Broadcast Global | Receive | Receive |
| **Feedback Desk** | Review All | Submit | Submit |

---

## 🛠️ Technology Stack

| Layer | Technology | Purpose |
| :--- | :--- | :--- |
| **Backend Framework** | `Python 3.8+` / `Django 4.2.24` | Core business logic, routing, and ORM layer |
| **Database** | `SQLite` (Dev) / `PostgreSQL` (Prod) | Relational data persistence and transactional integrity |
| **Frontend** | `HTML5`, `CSS3`, `JavaScript` | Dynamic user interfaces and responsive dashboards |
| **Authentication** | `Django Auth` + Custom Middleware | Role-segregated session access control |
| **Asset Pipeline** | `WhiteNoise` | Optimized static file streaming |
| **Communication** | `SMTP` / Gmail Relay | Automated alerts, reminders, and verification emails |

---

## 📂 Project Structure

```bash
student-erp-management-system/
├── main_app/                      # Core business logic application
│   ├── migrations/                # Database schema versioning
│   ├── static/                    # Component-level CSS, JavaScript, and icons
│   ├── templates/                 # Role-segregated HTML templates
│   ├── admin.py                   # Model registry for Django admin
│   ├── EditResultView.py          # Examination marks update engine
│   ├── EmailBackend.py            # Custom email authentication handler
│   ├── forms.py                   # Form validation and dynamic field controls
│   ├── hod_views.py               # Administrator operations controller
│   ├── middleware.py              # Role-based access control interceptor
│   ├── models.py                  # Relational database models
│   ├── staff_views.py             # Faculty operations controller
│   ├── student_views.py           # Student self-service controller
│   ├── urls.py                    # App endpoint routing
│   └── views.py                   # Base authentication and session views
├── student_management_system/     # Root application configuration
│   ├── settings.py                # Environment parameters and app registry
│   ├── urls.py                    # Root URL dispatcher
│   └── wsgi.py                    # WSGI gateway for web deployment
├── static/                        # Collected static files
├── media/                         # Uploaded user assets (profile images, receipts)
├── manage.py                      # Django execution entry point
├── requirements.txt               # Locked production dependencies
└── README.md                      # Repository documentation
```
##  🗃️ Database Schema Overview
```text
CustomUser (AbstractUser)
  ├── AdminProfile       ──> Institutional Operations & Approvals
  ├── StaffProfile       ──> Assigned Subjects, Leaves, Result Logging
  └── StudentProfile     ──> Course Mapping, Session, Attendance, Invoices
        │
        ├── AttendanceReport (FK: Attendance, Student)
        ├── StudentResult    (FK: Subject, Student)
        ├── StudentFee       (FK: Course, Student)
        └── LeaveReport      (FK: Student / Staff)
```
---

## 🚀 Quick Start Guide

### 1. Clone & Navigate

```bash
git clone [https://github.com/YOUR-USERNAME/student-erp-management-system.git](https://github.com/YOUR-USERNAME/student-erp-management-system.git)
cd student-erp-management-system
```

### 2. Set Up Virtual Environment

**Linux / macOS:**
```bash
python3 -m venv venv
source venv/bin/activate
```

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Database Setup & Initialization

```bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
python manage.py collectstatic --noinput
```

### 5. Run Development Server

```bash
python manage.py runserver
```

Open `http://127.0.0.1:8000/` in your browser.

---

## ⚙️ Configuration & Environment

Create a `.env` file in the project root directory to manage your environment-specific credentials:

```ini
SECRET_KEY=your_django_secret_key_here
DEBUG=True
ALLOWED_HOSTS=127.0.0.1,localhost

# Email Configuration (SMTP)
EMAIL_BACKEND=django.core.mail.backends.smtp.EmailBackend
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_HOST_USER=your-email@example.com
EMAIL_HOST_PASSWORD=your-app-specific-password
EMAIL_USE_TLS=True
```

---

## 🔒 Production Hardening Checklist

- [ ] Set `DEBUG = False` in production settings.
- [ ] Bind exact production domains inside `ALLOWED_HOSTS`.
- [ ] Migrate database from SQLite to **PostgreSQL**.
- [ ] Enforce SSL/HTTPS redirect rules.
- [ ] Configure `WhiteNoise` or Amazon S3 for static and media asset streaming.
- [ ] Ensure `.env` is listed inside `.gitignore` to protect sensitive credentials.

---

## 📈 Future Roadmap

- [ ] **Payment Gateway:** Direct online fee settlement via Stripe or Razorpay.
- [ ] **Timetable Engine:** Algorithmic clash-free classroom and lab scheduling.
- [ ] **Examinations:** Online timed assessments with automated grading.
- [ ] **Push Notifications:** Firebase Cloud Messaging integration for real-time mobile updates.
- [ ] **PDF Invoicing:** Automated fee receipts and marksheet export engines.

---

## 🤝 Contributing

1. **Fork** the repository.
2. Create a feature branch:
   ```bash
   git checkout -b feature/NewFeature
   ```
3. Commit your changes:
   ```bash
   git commit -m "feat: Add NewFeature functionality"
   ```
4. Push to the branch:
   ```bash
   git push origin feature/NewFeature
   ```
5. Open a **Pull Request**.

---

## 📜 License

Distributed under the **MIT License**. See `LICENSE` for more information.

---

## 👨‍💻 Author

**Ankit Kumar**  
*Student ERP Management System*  
*Built with ❤️ using Python & Django.*

<div align="center">

⭐ **If you find this project useful, please consider giving it a star on GitHub!** ⭐

</div>
