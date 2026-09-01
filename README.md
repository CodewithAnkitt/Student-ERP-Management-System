# Student Management System

A comprehensive web-based Student Management System built with Django that enables educational institutions to manage students, staff, courses, attendance, results, and communications efficiently.

## Features

### Admin (HOD) Features
- Manage staff members (add, edit, delete)
- Manage students (add, edit, delete)
- Manage courses and subjects
- Manage academic sessions
- View and manage attendance records
- Send notifications to students and staff
- Review and respond to feedback from students and staff
- Approve/reject leave applications
- View comprehensive dashboard with statistics

### Staff Features
- Take and update student attendance
- Add and edit student results (test and exam scores)
- Apply for leave
- Submit feedback to admin
- View assigned subjects and students
- Receive notifications from admin
- View personal profile

### Student Features
- View attendance records
- View exam results
- Apply for leave
- Submit feedback to admin
- Receive notifications from admin
- View personal profile and course information

## Technology Stack

- **Backend**: Django 4.2.24
- **Database**: SQLite (default), PostgreSQL/MySQL support available
- **Frontend**: HTML, CSS, JavaScript (templates)
- **Authentication**: Custom email-based authentication
- **File Storage**: WhiteNoise for static files
- **Email**: SMTP backend for notifications
- **Deployment**: Gunicorn-ready for production

## Prerequisites

- Python 3.8 or higher
- pip (Python package manager)
- Virtual environment (recommended)

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd student_management_system
```

2. Create and activate a virtual environment:
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux/Mac
python3 -m venv venv
source venv/bin/activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Configure environment variables (optional):
Create a `.env` file or update `settings.py` with your configurations:
- Database settings
- Email configuration
- Secret key
- Debug mode

5. Run migrations:
```bash
python manage.py makemigrations
python manage.py migrate
```

6. Create a superuser (admin):
```bash
python manage.py createsuperuser
```

7. Collect static files:
```bash
python manage.py collectstatic
```

8. Run the development server:
```bash
python manage.py runserver
```

9. Access the application at `http://127.0.0.1:8000/`

## Project Structure

```
student_management_system/
├── main_app/                   # Main application
│   ├── migrations/            # Database migrations
│   ├── static/                # Static files (CSS, JS, images)
│   ├── templates/             # HTML templates
│   ├── admin.py               # Admin configurations
│   ├── models.py              # Database models
│   ├── views.py               # Main views
│   ├── hod_views.py           # Admin/HOD views
│   ├── staff_views.py         # Staff views
│   ├── student_views.py       # Student views
│   ├── forms.py               # Form definitions
│   ├── urls.py                # URL routing
│   ├── middleware.py          # Custom middleware
│   ├── EmailBackend.py        # Email authentication backend
│   └── EditResultView.py      # Result editing view
├── student_management_system/ # Project settings
│   ├── settings.py            # Django settings
│   ├── urls.py                # Root URL configuration
│   ├── wsgi.py                # WSGI configuration
│   └── asgi.py                # ASGI configuration
├── media/                     # User uploaded files
├── static/                    # Collected static files
├── db.sqlite3                 # SQLite database
├── manage.py                  # Django management script
└── requirements.txt           # Python dependencies
```

## Database Models

- **CustomUser**: Extended user model with email authentication
- **Admin**: Admin/HOD profile
- **Staff**: Staff member profile
- **Student**: Student profile
- **Course**: Academic courses
- **Subject**: Course subjects
- **Session**: Academic sessions/years
- **Attendance**: Attendance records
- **AttendanceReport**: Individual student attendance
- **LeaveReportStudent**: Student leave applications
- **LeaveReportStaff**: Staff leave applications
- **FeedbackStudent**: Student feedback
- **FeedbackStaff**: Staff feedback
- **NotificationStudent**: Student notifications
- **NotificationStaff**: Staff notifications
- **StudentResult**: Student exam results

## User Roles

The system supports three user types:
1. **HOD (Head of Department)** - Admin with full access
2. **Staff** - Teachers/instructors with limited access
3. **Student** - Students with view and self-service access

## Authentication

- Email-based authentication (no username required)
- Custom authentication backend
- Role-based access control via middleware
- Session management

## Configuration

### Email Settings
Update the following in `settings.py`:
```python
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.gmail.com'
EMAIL_PORT = 587
EMAIL_HOST_USER = 'your-email@example.com'
EMAIL_HOST_PASSWORD = 'your-app-password'
EMAIL_USE_TLS = True
```

### Database Configuration
For production, configure PostgreSQL or MySQL:
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'your_db_name',
        'USER': 'your_db_user',
        'PASSWORD': 'your_db_password',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

## Deployment

The application is configured for deployment with:
- WhiteNoise for static file serving
- Gunicorn as WSGI server
- Database URL configuration via `dj-database-url`

For production deployment:
1. Set `DEBUG = False` in settings
2. Configure `ALLOWED_HOSTS`
3. Set up a production database
4. Configure a proper secret key
5. Set up email service
6. Use a production-grade web server (Nginx + Gunicorn)

## Security Notes

⚠️ **Important**: Before deploying to production:
- Change the `SECRET_KEY` in settings.py
- Set `DEBUG = False`
- Configure proper `ALLOWED_HOSTS`
- Use environment variables for sensitive data
- Enable password validators
- Set up HTTPS
- Configure CSRF and security middleware properly

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

This project is available for educational and commercial use.

## Support

For issues, questions, or contributions, please open an issue in the repository.
