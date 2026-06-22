# 💰 FinanceTracker

FinanceTracker is a Personal Finance Management Web Application built using Django. It helps users manage their income, expenses, budgets, accounts, and financial activities through an intuitive dashboard.

---

# 📌 Features

* User Registration & Login
* Income Management
* Expense Management
* Income Categories
* Expense Categories
* Account Management
* Budget Management
* Financial Dashboard
* User Profile Management
* Secure Authentication System
* User-specific Data Access

---

# 🛠️ Tech Stack

### Backend

* Python
* Django

### Frontend

* HTML5
* CSS3
* JavaScript
* Bootstrap

### Database

* SQLite3

---

# 📂 Project Structure

```text
FinanceTracker/
│
├── FinanceTracker/        # Project Configuration
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
├── FinTech/               # Main Application
│   ├── models.py
│   ├── views.py
│   ├── urls.py
│   ├── admin.py
│   └── migrations/
│
├── templates/             # HTML Templates
├── static/                # CSS, JavaScript, Images
├── db.sqlite3             # Database
├── manage.py              # Django Entry Point
└── requirements.txt       # Project Dependencies
```

---

# ⚙️ Installation Guide

## 1. Clone Repository

```bash
git clone https://github.com/ravikumarxworkz/FinanceTracker.git
cd FinanceTracker
```

---

## 2. Create Virtual Environment

```bash
python -m venv venv
```

---

## 3. Activate Virtual Environment

### Windows

```bash
.\venv\Scripts\activate
```

If you get execution policy restrictions:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
```

Then activate again:

```bash
.\venv\Scripts\activate
```

### Linux / Mac

```bash
source venv/bin/activate
```

---

## 4. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 5. Apply Database Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

---

## 6. Create Superuser

```bash
python manage.py createsuperuser
```

Enter:

```text
Username:
Email:
Password:
```

---

## 7. Run Application

```bash
python manage.py runserver
```

---

# 🌐 Application URLs

## Main Application

```text
http://127.0.0.1:8000/
```

## Django Admin

```text
http://127.0.0.1:8000/admin/
```

The Django Admin Panel allows administrators to manage:

* Users
* Income Categories
* Expense Categories
* Income Records
* Expense Records
* Accounts
* Budgets

Login using the superuser credentials created with:

```bash
python manage.py createsuperuser
```

---

# 📊 Modules

## Dashboard

Provides:

* Current Account Balance
* Income Overview
* Expense Overview
* Category-wise Expense Analysis
* Financial Statistics

---

## Income Management

Features:

* Add Income
* Edit Income
* Delete Income
* View Income History
* Categorize Income Sources

Examples:

* Salary
* Freelancing
* Business
* Investments

---

## Expense Management

Features:

* Add Expense
* Edit Expense
* Delete Expense
* Expense History
* Category Tracking

Examples:

* Food
* Transport
* Shopping
* Bills
* Entertainment

---

## Category Management

Users can create:

### Income Categories

* Salary
* Business
* Freelance
* Investments

### Expense Categories

* Food
* Travel
* Education
* Healthcare

---

## Account Management

Manage:

* Account Name
* Current Balance
* Account Details

Examples:

* Savings Account
* Current Account
* Cash Wallet

---

## Budget Management

Users can:

* Create Budgets
* Track Spending Limits
* Monitor Budget Utilization

---

# 🔒 Security Features

* Django Authentication System
* Password Hashing
* Session Management
* CSRF Protection
* User-specific Data Isolation

---

# 🗄️ Database Models

### User

Stores authentication and profile information.

### IncomeCategory

Stores income category information.

### ExpenseCategory

Stores expense category information.

### Income

Stores income transactions.

### Expense

Stores expense transactions.

### Account

Stores account details and balances.

### Budget

Stores budget information.

---

# 🚀 Future Enhancements

* Export Reports to PDF
* Export Reports to Excel
* Monthly Financial Reports
* Email Notifications
* REST API Integration
* Mobile Responsive Dashboard
* Dark Mode Support

---

# 👨‍💻 Author

### Ravikumar Shankar Kumbar
* Dot net Developer
* Java Full Stack Developer
* Python Developer
* Django Developer


GitHub:
https://github.com/ravikumarxworkz

---

# 📜 License

This project is developed for learning and educational purposes.
