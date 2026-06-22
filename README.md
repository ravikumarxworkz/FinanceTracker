# 💰 FinanceTracker

FinanceTracker is a Personal Finance Management Web Application built with Django. It helps users manage income, expenses, budgets, accounts, and financial reports in a simple and secure way.

## 🚀 Features

* User Registration & Authentication
* Income Management
* Expense Management
* Income & Expense Categories
* Account Management
* Budget Tracking
* Financial Dashboard
* Reports & Analytics
* User Profile Management
* Secure User-Specific Data

---

## 🛠️ Technology Stack

* Python 3.x
* Django 4.x
* SQLite3
* HTML5
* CSS3
* JavaScript
* Bootstrap

---

## 📂 Project Structure

```text
FinanceTracker/
│
├── FinanceTracker/      # Project Configuration
├── FinTech/             # Main Application
├── templates/           # HTML Templates
├── static/              # CSS, JS, Images
├── db.sqlite3           # Database
├── manage.py            # Django Entry Point
└── requirements.txt     # Project Dependencies
```

---

## ⚙️ Installation & Setup

### 1. Clone Repository

```bash
git clone https://github.com/your-username/FinanceTracker.git
cd FinanceTracker
```

### 2. Create Virtual Environment

```bash
python -m venv venv
```

### 3. Activate Virtual Environment

#### Windows

```bash
.\venv\Scripts\activate
```

If you get an execution policy error:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
```

Then activate again:

```bash
.\venv\Scripts\activate
```

#### Linux / Mac

```bash
source venv/bin/activate
```

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

### 5. Run Database Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### 6. Create Admin User (Optional)

```bash
python manage.py createsuperuser
```

### 7. Start Development Server

```bash
python manage.py runserver
```

---

## 🌐 Application URLs

### Main Application

```text
http://127.0.0.1:8000/
```

### Django Admin

```text
http://127.0.0.1:8000/admin/
```

---

## 📊 Core Modules

### Income Management

* Add Income
* Update Income
* Delete Income
* View Income History

### Expense Management

* Add Expense
* Update Expense
* Delete Expense
* View Expense History

### Category Management

* Income Categories
* Expense Categories

### Account Management

* Track Account Balance
* Balance Updates Based on Transactions

### Dashboard

* Financial Summary
* Expense Analytics
* Income Analytics
* Charts & Reports

---

## 🔐 Security

* Django Authentication System
* Session-Based Login
* User-Specific Data Access
* CSRF Protection

---

## 👨‍💻 Author

**Ravikumar Shankar Kumbar**

Java Full Stack Developer | Python Developer

---

## 📜 License

This project is for learning and educational purposes.
