# FinanceTracker Project - Complete Explanation Guide

## 📋 Project Overview

**FinanceTracker** is a **Personal Finance Management Web Application** built using Django framework. It helps users track their income, expenses, budgets, and accounts efficiently.

### Key Features:
- ✅ User Authentication (Sign up, Login, Logout)
- 💰 Income & Expense Tracking
- 📊 Dashboard with Charts & Analytics
- 📂 Category Management (Income & Expense Categories)
- 💳 Account Management
- 📈 Financial Reports
- 👤 User Profile Settings
- 🔐 Secure User-specific Data

---

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                     FRONTEND (HTML/CSS/JS)                   │
│                   - Templates (HTML Pages)                   │
│                   - Static Files (CSS/JS)                    │
└────────────────────────┬────────────────────────────────────┘
                         │ HTTP Requests/Responses
                         ↓
┌─────────────────────────────────────────────────────────────┐
│              MIDDLEWARE & URL ROUTING (Django)               │
│                   - urls.py (Route Mapping)                  │
│                   - Middleware (Security)                    │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ↓
┌─────────────────────────────────────────────────────────────┐
│                  VIEWS (Business Logic)                      │
│         - views.py (Controllers for each feature)            │
│         - Request Processing                                │
│         - Data Validation                                   │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ↓
┌─────────────────────────────────────────────────────────────┐
│                   MODELS (Database Layer)                    │
│          - User, Income, Expense, Category                  │
│          - Account, Budget                                  │
└────────────────────────┬────────────────────────────────────┘
                         │ Database Queries
                         ↓
┌─────────────────────────────────────────────────────────────┐
│              DATABASE (SQLite - db.sqlite3)                  │
│          - Stores all application data                      │
└─────────────────────────────────────────────────────────────┘
```

---

## 📁 Project Structure Breakdown

```
FinanceTracker/                          # Main Project Folder
├── FinanceTracker/                      # Main Application Config
│   ├── settings.py                      # App Configuration
│   ├── urls.py                          # Main URL Routes
│   ├── wsgi.py                          # Web Server Gateway
│   └── asgi.py                          # Async Web Server
│
├── FinTech/                             # Main App (Business Logic)
│   ├── models.py                        # Database Models
│   ├── views.py                         # Business Logic (461 lines)
│   ├── urls.py                          # App Routes
│   ├── admin.py                         # Django Admin
│   └── migrations/                      # Database Migrations
│
├── templates/                           # HTML Pages
│   ├── index.html                       # Landing Page
│   ├── dashboard.html                   # Dashboard
│   ├── income.html                      # Income Management
│   ├── expense.html                     # Expense Management
│   ├── profile.html                     # User Profile
│   └── settings.html                    # Settings Page
│
├── static/                              # Frontend Files
│   ├── styles.css                       # Global Styles
│   ├── dashboard.js                     # Dashboard Logic
│   ├── script.js                        # Global Scripts
│   └── (other CSS/JS files)
│
├── db.sqlite3                           # Database File
├── manage.py                            # Django Management
└── requirements.txt                     # Dependencies
```

---

## 🗄️ Database Models (Data Structure)

### 1. **User Model** (Django Built-in)
```python
# Provided by Django
- id (Primary Key)
- username
- password
- email
- first_name
- last_name
```

### 2. **IncomeCategory Model**
```python
Fields:
- id (Primary Key)
- name (CharField) - Category name (e.g., "Salary", "Freelance")
- user (ForeignKey) - Links to User who owns this category
```

### 3. **ExpenseCategory Model**
```python
Fields:
- id (Primary Key)
- name (CharField) - Category name (e.g., "Food", "Transport")
- user (ForeignKey) - Links to User who owns this category
```

### 4. **Income Model**
```python
Fields:
- id (Primary Key)
- user (ForeignKey) - Links to the user
- name (CharField) - Income description
- date (DateField) - Income date
- amount (FloatField) - Amount received
- category (ForeignKey) - Links to IncomeCategory
- note (TextField) - Additional notes
```

### 5. **Expense Model**
```python
Fields:
- id (Primary Key)
- user (ForeignKey) - Links to the user
- name (CharField) - Expense description
- date (DateField) - Expense date
- amount (FloatField) - Amount spent
- category (ForeignKey) - Links to ExpenseCategory
- note (TextField) - Additional notes
```

### 6. **Account Model**
```python
Fields:
- id (Primary Key)
- user (ForeignKey) - Links to the user
- name (CharField) - Account name (e.g., "Savings", "Checking")
- balance (FloatField) - Current balance
- details (CharField) - Account details
```

### 7. **Budget Model**
```python
Fields:
- id (Primary Key)
- user (ForeignKey) - Links to the user
- name (CharField) - Budget name
- balance (FloatField) - Budget amount
- details (CharField) - Budget details
```

### Database Relationships Diagram:
```
┌─────────────┐
│    User     │
└──────┬──────┘
       │
       ├─────┬─────────┬──────────┬──────────┐
       │     │         │          │          │
       ↓     ↓         ↓          ↓          ↓
    Income Category  Expense   Account    Budget
    Expense Income   Expense
```

---

## 🔄 Complete Data Flow: Frontend to Backend

### Flow Diagram:
```
USER ACTION (Frontend)
       ↓
HTML Form Submission
       ↓
HTTP Request (GET/POST)
       ↓
Django URL Router (urls.py)
       ↓
View Function (views.py)
       ↓
Database Query (models.py)
       ↓
SQLite Database
       ↓
Response with Data
       ↓
Template Rendering (HTML)
       ↓
Response to Browser
       ↓
Browser Displays Page
```

---

## 📌 Detailed Use Case Examples

### **Use Case 1: User Adding an Expense**

#### Step 1: Frontend (HTML Form)
```html
<!-- expense.html -->
<form method="POST" action="/expenses">
    <input type="text" name="name" placeholder="Expense name">
    <input type="number" name="amount" placeholder="Amount">
    <select name="category">
        <option>Select Category</option>
        <!-- Categories from backend -->
    </select>
    <input type="date" name="date">
    <textarea name="note"></textarea>
    <button type="submit">Add Expense</button>
</form>
```

**User fills form and clicks submit** → Browser sends POST request

#### Step 2: URL Routing (urls.py)
```python
path('expenses', views.expenses, name="expenses"),
# Django matches /expenses to expenses view function
```

#### Step 3: View Processing (views.py)
```python
def expenses(request):
    if request.user.is_authenticated:
        if request.method == "POST":
            # Get form data from request
            name = request.POST['name']
            category_id = request.POST.get('category')
            amount = request.POST['amount']
            date = request.POST['date']
            note = request.POST.get('note')
            
            # Get category from database
            category = ExpenseCategory.objects.get(
                user=request.user.id, 
                id=int(category_id)
            )
            
            # Update account balance (deduct expense)
            my_account = Account.objects.get(user=request.user.id)
            my_account.balance -= float(amount)  # ← IMPORTANT
            my_account.save()
            
            # Create new expense record
            Expense.objects.create(
                name=name,
                user=request.user,
                category=category,
                amount=amount,
                date=date,
                note=note
            )
            return redirect('/expenses')  # Redirect to expenses page
```

#### Step 4: Database Operations
```
1. Query: SELECT * FROM FinTech_expensecategory 
          WHERE user_id = 5 AND id = 2
   Result: Get the selected category

2. Query: SELECT * FROM FinTech_account 
          WHERE user_id = 5
   Result: Get user's account

3. Update: UPDATE FinTech_account 
           SET balance = balance - 500 
           WHERE user_id = 5
   Result: Balance reduced

4. Insert: INSERT INTO FinTech_expense 
           (name, user_id, category_id, amount, date, note) 
           VALUES ('Lunch', 5, 2, 500, '2025-11-30', 'At Cafe')
   Result: New expense created
```

#### Step 5: Response & Display
- View redirects to `/expenses`
- Django fetches all expenses for current user
- Template renders with updated expense list
- Browser displays the page with new expense added

---

### **Use Case 2: Viewing Dashboard**

#### Step 1: User visits /dashboard
```
Browser URL: http://localhost:8000/dashboard
```

#### Step 2: URL Routing
```python
path('dashboard', views.dashboard, name="dashboard")
```

#### Step 3: View Processing
```python
def dashboard(request):
    if request.user.is_authenticated:
        # 1. Get user's account balance
        my_account = Account.objects.get(user=request.user.id)
        balance = my_account.balance
        
        # 2. Calculate expenses by category
        out_dict = {}
        my_catg = ExpenseCategory.objects.filter(user=request.user.id)
        for catg in my_catg:
            out_dict[catg.name] = 0
        
        # Sum up expenses for each category
        expenses = Expense.objects.filter(user=request.user.id)
        for expense in expenses:
            out_dict[expense.category.name] += expense.amount
        
        # 3. Get last 10 days income data
        Income_last_10days_amount = []
        for i in range(10):
            _10days_income = Income.objects.filter(
                user=request.user.id,
                date__gte=date.today()-timedelta(days=i),
                date__lt=date.today()-timedelta(days=i-1)
            )
            total_of_aday = sum([inc.amount for inc in _10days_income])
            Income_last_10days_amount.append(total_of_aday)
        
        # 4. Similar for expenses (10 days)
        # 5. Format dates
        # 6. Send data to template
        return render(request, "dashboard.html", {
            "balance": balance,
            "category_list": catg_list,
            "catg_total_list": catg_total_list,
            "pre_10days_list": pre_10days_list,
            "Income_last_10days_amount": Income_last_10days_amount,
            "Expense_last_10days_amount": Expense_last_10days_amount
        })
```

#### Step 4: Template Rendering
```html
<!-- dashboard.html -->
<h1>Your Balance: Rs. {{ balance }}</h1>

<!-- Chart showing expense categories -->
{% for category in category_list %}
    <div>{{ category }}: Rs. {{ catg_total_list.0 }}</div>
{% endfor %}

<!-- Chart showing last 10 days -->
<script>
    // JavaScript uses data from backend to draw charts
    const incomeData = {{ Income_last_10days_amount }};
    const expenseData = {{ Expense_last_10days_amount }};
    // Draw charts using Chart.js or similar library
</script>
```

---

## 🔑 Key Django Concepts

### 1. **URL Routing (urls.py)**
Maps URL patterns to view functions
```python
urlpatterns = [
    path('dashboard', views.dashboard, name="dashboard"),
    path('expenses', views.expenses, name="expenses"),
]
```

### 2. **Views (views.py)**
- Handle HTTP requests
- Process business logic
- Query database
- Return responses

### 3. **Models (models.py)**
- Define database tables
- Define relationships between tables
- Provide database query interface (ORM)

### 4. **Templates (HTML)**
- Display data to users
- Collect form input
- Template variables: `{{ variable_name }}`
- Template loops: `{% for item in list %}`

### 5. **Authentication**
```python
if request.user.is_authenticated:  # Check if user is logged in
    # Allow access
else:
    return redirect("/")  # Redirect to login
```

---

## 🔐 Security Features

### 1. **User Authentication**
- Django's built-in User model
- Password hashing
- Session management

### 2. **Authorization**
- `is_authenticated` check ensures only logged-in users can access features
- Each user only sees their own data (filtered by `user_id`)

### 3. **CSRF Protection**
- Every form has CSRF token
- Middleware: `CsrfViewMiddleware`

### 4. **Data Isolation**
```python
# Each user only sees their own data
expenses = Expense.objects.filter(user=request.user.id)
```

---

## 📊 Important Queries in the Application

### Get User's Expenses
```python
expenses = Expense.objects.filter(user=request.user.id)
```

### Get Specific Expense by ID
```python
expense = Expense.objects.get(id=expense_id)
```

### Get Expenses for Last 10 Days
```python
from datetime import date, timedelta
recent_expenses = Expense.objects.filter(
    user=request.user.id,
    date__gte=date.today()-timedelta(days=10)
)
```

### Get Expenses by Category
```python
expenses_by_category = Expense.objects.filter(
    user=request.user.id,
    category=category_id
)
```

### Calculate Total Expenses
```python
total = sum([exp.amount for exp in expenses])
```

---

## 🌐 Complete Request-Response Cycle Example

```
┌─────────────────────────────────────────────────────────────┐
│ STEP 1: USER ACTION (Browser)                              │
├─────────────────────────────────────────────────────────────┤
│ User clicks "Add Expense" button                            │
│ Form gets filled:                                           │
│   - Name: "Lunch"                                           │
│   - Amount: 500                                             │
│   - Category: "Food" (id=2)                                 │
│   - Date: "2025-11-30"                                      │
└─────────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 2: HTTP REQUEST (Browser → Server)                    │
├─────────────────────────────────────────────────────────────┤
│ POST /expenses HTTP/1.1                                     │
│ Host: localhost:8000                                        │
│ Content-Type: application/x-www-form-urlencoded            │
│                                                              │
│ Body:                                                        │
│ name=Lunch&amount=500&category=2&date=2025-11-30&note=Cafe│
└─────────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 3: URL ROUTING (Django)                               │
├─────────────────────────────────────────────────────────────┤
│ URL: /expenses matches pattern in urls.py                  │
│ Matched function: views.expenses                            │
│ Request forwarded to: def expenses(request)                │
└─────────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 4: VIEW PROCESSING (Business Logic)                   │
├─────────────────────────────────────────────────────────────┤
│ 1. Check if user is authenticated                          │
│ 2. Check if request.method == "POST"                       │
│ 3. Extract form data:                                       │
│    name = "Lunch"                                           │
│    amount = "500"                                           │
│    category_id = "2"                                        │
│ 4. Query category: ExpenseCategory.objects.get(id=2)      │
│ 5. Query account: Account.objects.get(user=current_user)  │
│ 6. Update balance: balance = balance - 500                 │
│ 7. Create expense: Expense.objects.create(...)            │
└─────────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 5: DATABASE OPERATIONS (SQLite)                       │
├─────────────────────────────────────────────────────────────┤
│ Transaction 1:                                              │
│ SELECT * FROM FinTech_expensecategory WHERE id=2           │
│ Result: Food category object                               │
│                                                              │
│ Transaction 2:                                              │
│ SELECT * FROM FinTech_account WHERE user_id=current_user   │
│ Result: User's account                                      │
│                                                              │
│ Transaction 3:                                              │
│ UPDATE FinTech_account SET balance=balance-500             │
│ Result: Balance updated                                     │
│                                                              │
│ Transaction 4:                                              │
│ INSERT INTO FinTech_expense(...) VALUES(...)               │
│ Result: Expense created                                     │
└─────────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 6: RESPONSE (Server → Browser)                        │
├─────────────────────────────────────────────────────────────┤
│ Redirect to: /expenses                                      │
│ HTTP/1.1 302 Found                                          │
│ Location: /expenses                                         │
└─────────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 7: FOLLOW REDIRECT (Browser)                          │
├─────────────────────────────────────────────────────────────┤
│ GET /expenses HTTP/1.1                                      │
└─────────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 8: FETCH EXPENSES (View Processing)                   │
├─────────────────────────────────────────────────────────────┤
│ Query: Expense.objects.filter(user=current_user)          │
│ Result: All expenses including the newly created one       │
│ Render template with expense data                          │
└─────────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 9: TEMPLATE RENDERING (HTML)                          │
├─────────────────────────────────────────────────────────────┤
│ Loop through expenses:                                      │
│ {% for expense in expenses %}                              │
│   - Lunch: 500 (Food)                                       │
│   - Previous expenses...                                    │
│ {% endfor %}                                                │
└─────────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 10: HTTP RESPONSE (Browser)                           │
├─────────────────────────────────────────────────────────────┤
│ HTTP/1.1 200 OK                                             │
│ Content-Type: text/html                                     │
│                                                              │
│ <html>                                                       │
│   <body>                                                     │
│     <h1>Expenses</h1>                                        │
│     <table>                                                  │
│       <tr>                                                   │
│         <td>Lunch</td>                                       │
│         <td>500</td>                                         │
│         <td>Food</td>                                        │
│       </tr>                                                  │
│     </table>                                                 │
│   </body>                                                    │
│ </html>                                                      │
└─────────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────────┐
│ STEP 11: BROWSER RENDERING                                 │
├─────────────────────────────────────────────────────────────┤
│ Browser displays:                                           │
│                                                              │
│ ┌─────────────────────┐                                     │
│ │     Expenses        │                                     │
│ ├─────────────────────┤                                     │
│ │ Lunch | 500 | Food  │ ← NEW EXPENSE VISIBLE              │
│ │ ...                 │                                     │
│ └─────────────────────┘                                     │
│                                                              │
│ ✅ User sees their new expense!                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 🔍 How Each Feature Works

### **Feature 1: Dashboard**
```
1. User clicks dashboard link
2. View fetches: account balance, expense categories, last 10 days data
3. Calculates: total expenses per category, daily income/expense totals
4. Sends data to template with charts (using JavaScript)
5. Dashboard displays financial overview
```

### **Feature 2: Add Income**
```
1. User fills income form (name, amount, date, category)
2. POST request sent to /incomes
3. View validates category ownership (security)
4. Account balance INCREASED by income amount
5. New Income record created in database
6. Page redirects to income list
7. User sees their income added
```

### **Feature 3: Add Expense**
```
1. User fills expense form
2. POST request sent to /expenses
3. View validates category ownership
4. Account balance DECREASED by expense amount
5. New Expense record created
6. Page redirects to expense list
7. User sees their expense added
```

### **Feature 4: Edit Expense**
```
1. User clicks edit on an expense
2. GET /edit-expense/<id> loads edit form
3. Current expense data populated in form
4. User modifies and submits
5. View calculates balance difference
6. If new amount > old: deduct difference
7. If new amount < old: add difference back
8. Expense updated in database
9. Redirect to expense list
```

### **Feature 5: Delete Expense**
```
1. User clicks delete button
2. GET /delete-expense/<id> triggered
3. View fetches expense amount
4. Account balance INCREASED (refund the expense)
5. Expense record deleted
6. Redirect to expense list
```

### **Feature 6: Category Management**
```
1. User adds new category
2. New IncomeCategory or ExpenseCategory created
3. Linked to current user
4. Later, user can select this category when adding income/expense
5. Multiple categories allow better expense tracking
```

---

## 📝 Important Code Concepts

### **1. Foreign Keys (Relationships)**
```python
# ExpenseCategory linked to User
class ExpenseCategory(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    # If user deleted, all their categories deleted too

# Expense linked to User and Category
class Expense(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    category = models.ForeignKey(ExpenseCategory, on_delete=models.CASCADE)
```

### **2. Filtering Data (User-specific)**
```python
# Get only current user's expenses
expenses = Expense.objects.filter(user=request.user.id)

# This ensures users can't see others' data
```

### **3. Form Processing (POST Request)**
```python
if request.method == "POST":
    # Access form data
    name = request.POST['name']
    amount = request.POST['amount']
    # Process the data
```

### **4. Database Transactions**
```python
# Get the account
account = Account.objects.get(user=request.user.id)

# Modify the balance
account.balance -= float(amount)

# Save changes to database
account.save()
```

### **5. Redirects (Navigation)**
```python
# After adding expense, redirect to expense list
return redirect('/expenses')
```

---

## 🎓 Learning Path for Students

### **Level 1: Beginner**
- Understand what Django is (Web Framework)
- Understand MTV architecture (Models-Templates-Views)
- Learn what a database is (SQLite)
- Learn what HTTP is (Requests and Responses)

### **Level 2: Intermediate**
- Understand Django Models (Database tables)
- Understand Django Views (Business logic)
- Understand Django Templates (HTML pages)
- Understand URL routing

### **Level 3: Advanced**
- Understand Foreign Keys and relationships
- Understand QuerySets (Database queries)
- Understand authentication/authorization
- Understand form processing

### **Level 4: Expert**
- Optimize database queries (select_related, prefetch_related)
- Implement complex business logic
- Handle edge cases and error handling
- Deploy to production

---

## 🚀 How to Run This Project

### Step 1: Setup Virtual Environment
```bash
python -m venv venv
.\venv\Scripts\activate  # Windows
```

### Step 2: Install Dependencies
```bash
pip install -r requirements.txt
```

### Step 3: Run Database Migrations
```bash
python manage.py migrate
```

### Step 4: Create Superuser (Admin)
```bash
python manage.py createsuperuser
```

### Step 5: Run Development Server
```bash
python manage.py runserver
```

### Step 6: Access the Application
```
- Main App: http://localhost:8000
- Admin Panel: http://localhost:8000/admin
```

---

## 💡 Key Takeaways

1. **Frontend (HTML/CSS)** → User Interface
2. **URL Routing** → Maps URLs to functions
3. **Views** → Business logic (process requests)
4. **Models** → Database structure and queries
5. **Database** → Persistent data storage
6. **Templates** → Render HTML with dynamic data
7. **Authentication** → Secure user login
8. **Authorization** → User can only access their own data

---

## 📚 Additional Concepts

### **REST vs Traditional Web App**
- This project uses **Traditional Web App** approach
- Forms submit to backend, page reloads with new data
- Not a REST API (no JSON endpoints for frontend)

### **MVC vs MTV**
- Django uses **MTV** (Models-Templates-Views)
- Models = Database layer
- Templates = View layer (UI)
- Views = Controller layer (Business logic)

### **Stateless vs Stateful**
- This app is **Stateful** (uses sessions)
- User login creates session
- Session persists across multiple requests

---

## 🎯 Summary

FinanceTracker is a complete web application that demonstrates:
- ✅ User authentication and authorization
- ✅ CRUD operations (Create, Read, Update, Delete)
- ✅ Database relationships (Foreign Keys)
- ✅ Request-response cycle
- ✅ Template rendering with dynamic data
- ✅ Form processing
- ✅ Data validation and security

**Perfect for learning Django web development!**

