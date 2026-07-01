# PeopleDesk — Employee Management Dashboard

A Django web application for managing employee records, organizing departments, and tracking workforce statistics through a responsive dashboard UI.

## Tech Stack

Python, Django, HTML5, CSS3 (no frontend framework — server-rendered templates), Chart.js (via CDN) for the two analytics charts on the dashboard.

## Features

- **Authentication** — login-protected dashboard; all pages require a logged-in user.
- **Dashboard home** — total employees, active employees, department count, and new hires this month, plus a department headcount bar chart and an active/inactive donut chart.
- **Employee management** — add, edit, delete, and view detailed employee records, with search by name/email/designation and filters by department and status.
- **Department management** — create departments, view per-department headcount (active vs. other), and delete departments.
- **Validated forms** — server-side validation (e.g. salary must be positive, joining date can't be in the future, minimum name length) with inline error messages.
- **Responsive layout** — collapsible sidebar on smaller screens, fluid stat/card grids.

## Project Structure

```
employee_dashboard/
├── manage.py
├── requirements.txt
├── employee_dashboard/        # project settings, root urls
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py / asgi.py
├── dashboard/                  # main app
│   ├── models.py               # Department, Employee
│   ├── forms.py                # EmployeeForm, DepartmentForm, StyledLoginForm
│   ├── views.py                # dashboard + CRUD views
│   ├── urls.py
│   ├── admin.py
│   └── migrations/
├── templates/
│   ├── base.html                # sidebar + topbar shell
│   ├── login.html
│   ├── dashboard.html
│   ├── employees.html
│   ├── add_employee.html
│   ├── edit_employee.html
│   ├── employee_detail.html
│   ├── departments.html
│   └── confirm_delete.html
└── static/
    ├── css/style.css
    └── js/main.js
```

## Setup

1. **Create a virtual environment and install dependencies:**

   ```bash
   python -m venv venv
   source venv/bin/activate   # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

2. **Apply migrations:**

   ```bash
   python manage.py migrate
   ```

3. **Create an admin account** (this is the login used for the dashboard itself, not just `/admin/`):

   ```bash
   python manage.py createsuperuser
   ```

4. **Run the development server:**

   ```bash
   python manage.py runserver
   ```

5. Visit `http://127.0.0.1:8000/` — you'll be redirected to the login page. Sign in with the superuser credentials you just created. The Django admin is also available at `/admin/` if you want to manage data directly.

## Notes for going to production

- Set `DEBUG = False` and update `ALLOWED_HOSTS` in `employee_dashboard/settings.py`.
- Move `SECRET_KEY` to an environment variable.
- Run `python manage.py collectstatic` and serve the `staticfiles/` directory with your web server or a tool like WhiteNoise.
- Swap the default SQLite database for Postgres/MySQL by updating `DATABASES` in `settings.py`.
