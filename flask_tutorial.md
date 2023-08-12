# Python Flask Intermediate Tutorial

## Table of Contents

1. **Introduction to Flask**

   - What is Flask?
   - Why use Flask?
   - Getting Started

2. **Routes and Views**

   - Creating Routes
   - Returning Views
   - Variable Rules
   - URL Building

3. **Templates and Jinja2**

   - Rendering Templates
   - Using Jinja2
   - Template Inheritance

4. **Forms and User Input**

   - Handling Forms
   - Validating Data
   - Flash Messages

5. **Database Integration**

   - Connecting to a Database
   - Models and ORM
   - CRUD Operations

6. **User Authentication**
   - User Registration
   - User Login
   - Protecting Routes

---

## 1. Introduction to Flask

### What is Flask?

Flask is a micro web framework for Python. It's designed to be simple and lightweight, allowing developers to build web applications quickly and easily.

### Why use Flask?

- Minimal Boilerplate: Flask keeps things simple and doesn't impose many restrictions.
- Flexibility: Choose your preferred tools and libraries for various components.
- Extensible: Add extensions and customize functionality as needed.

### Getting Started

1. Install Flask: `pip install Flask`
2. Create a new Python file, e.g., `app.py`.
3. Import Flask and create an instance of the app:

   ```python
   from flask import Flask

   app = Flask(__name__)
   ```

---

## 2. Routes and Views

### Creating Routes

Define routes using the `@app.route` decorator:

```python
@app.route('/')
def index():
    return "Hello, Flask!"
```

### Returning Views

Return HTML content using templates:

```python
from flask import render_template

@app.route('/home')
def home():
    return render_template('home.html')
```

### Variable Rules

Pass variables through URLs:

```python
@app.route('/user/<username>')
def show_user(username):
    return f"User: {username}"
```

### URL Building

Generate URLs using `url_for` function:

```python
from flask import url_for

@app.route('/about')
def about():
    return "This is the about page. <a href='" + url_for('home') + "'>Home</a>"
```

---

## 3. Templates and Jinja2

### Rendering Templates

Create templates using HTML and Jinja2 placeholders:

```html
<!-- templates/home.html -->
<!DOCTYPE html>
<html>
  <head>
    <title>Home</title>
  </head>
  <body>
    <h1>Welcome to our website</h1>
  </body>
</html>
```

### Using Jinja2

Use Jinja2 syntax for dynamic content in templates:

```html
<!-- templates/greeting.html -->
<!DOCTYPE html>
<html>
  <head>
    <title>Greeting</title>
  </head>
  <body>
    <h1>Hello, {{ name }}!</h1>
  </body>
</html>
```

In the view function:

```python
@app.route('/greet/<name>')
def greet(name):
    return render_template('greeting.html', name=name)
```

### Template Inheritance

Create a base template with common elements and extend it:

```html
<!-- templates/base.html -->
<!DOCTYPE html>
<html>
  <head>
    <title>{% block title %}{% endblock %}</title>
  </head>
  <body>
    <div class="content">{% block content %}{% endblock %}</div>
  </body>
</html>
```

Create a child template:

```html
<!-- templates/about.html -->
{% extends 'base.html' %} {% block title %}About{% endblock %} {% block content
%}
<h1>About Us</h1>
<p>We are a fantastic company!</p>
{% endblock %}
```

---

## 4. Forms and User Input

### Handling Forms

Create a form in HTML and handle submissions:

```html
<form method="POST" action="{{ url_for('submit_form') }}">
  <input type="text" name="username" />
  <button type="submit">Submit</button>
</form>
```

In the view function:

```python
from flask import request

@app.route('/form', methods=['GET', 'POST'])
def submit_form():
    if request.method == 'POST':
        username = request.form.get('username')
        return f"Submitted: {username}"
    return render_template('form.html')
```

### Validating Data

Use Flask-WTF to create and validate forms easily:

```python
from flask_wtf import FlaskForm
from wtforms import StringField, validators

class MyForm(FlaskForm):
    username = StringField('Username', [validators.DataRequired()])
```

### Flash Messages

Show flash messages for user feedback:

```python
from flask import flash

@app.route('/message')
def show_message():
    flash('This is a flash message!', 'success')
    return render_template('message.html')
```

In the template:

```html
{% with messages = get_flashed_messages() %} {% if messages %}
<ul class="flash">
  {% for message in messages %}
  <li>{{ message }}</li>
  {% endfor %}
</ul>
{% endif %} {% endwith %}
```

---

## 5. Database Integration

### Connecting to a Database

Use SQLAlchemy to interact with databases:

```python
from flask_sqlalchemy import SQLAlchemy

app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///mydatabase.db'
db = SQLAlchemy(app)
```

### Models and ORM

Define models using SQLAlchemy's ORM:

```python
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)
```

### CRUD Operations

Interact with the database using models:

```python
# Create
new_user = User(username='john_doe')
db.session.add(new_user)
db.session.commit()

# Read
user = User.query.filter_by(username='john_doe').first()

# Update
user.username = 'jane_doe'
db.session.commit()

# Delete
db.session.delete(user)
db.session.commit()
```

---

## 6. User Authentication

### User Registration

Create a registration form and store user credentials securely:

```python
from werkzeug.security import generate_password_hash

class User(db.Model):
    # ...
    password = db.Column(db.String(128), nullable=False)

hashed_password = generate_password_hash(password, method='sha256')
new_user = User(username='jane_doe', password=hashed_password)
db.session.add(new_user)
db.session.commit()
```

### User Login

Authenticate users during login:

```python
from werkzeug.security import check_password_hash
from flask_login import UserMixin

class User(UserMixin, db.Model):
    # ...

def verify_user(username, password):
    user = User.query.filter_by(username=username).first()
    if user and check_password_hash(user.password, password):
        return user
```

### Protecting Routes

Use Flask-Login to protect routes:

```python
from flask_login import login_required

@app.route('/dashboard')
@login_required
def dashboard():
    return "Welcome to your dashboard!"
```

---

Congratulations! You've completed the Python Flask Intermediate Tutorial. You've learned about routes, templates, forms, database integration, and user authentication using Flask. With this knowledge, you can

build more complex web applications and continue exploring Flask's extensive ecosystem of extensions and libraries.
