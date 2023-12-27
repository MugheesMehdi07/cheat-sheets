
# Flask Cheat Sheet

## Setup and Installation

```bash
# Install Flask
pip install flask

# Create a new Flask app
mkdir myflaskapp
cd myflaskapp
touch app.py
```

## Basic App Structure

```python
# app.py
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return 'Hello, Flask!'

if __name__ == '__main__':
    app.run(debug=True)
```

## Running the App

```bash
# Set environment variable
export FLASK_APP=app.py

# Run the app
flask run
# or
python -m flask run
```

## Routes and Views

```python
@app.route('/hello')
def hello():
    return 'Hello, World!'

@app.route('/user/<username>')
def show_user_profile(username):
    # show the user profile for that user
    return f'User {username}'
```

## Templates

- Create a `templates` folder in your project directory.
- Use Jinja2 template engine.

```html
<!-- templates/hello.html -->
<html>
  <head>
    <title>Flask App</title>
  </head>
  <body>
    <h1>Hello {{ name }}!</h1>
  </body>
</html>
```

```python
from flask import render_template

@app.route('/hello/<name>')
def hello_name(name):
    return render_template('hello.html', name=name)
```

## Static Files

- Place static files like CSS, JavaScript, images in a `static` folder.

```html
<link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
```

## Request Data

```python
from flask import request

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        # handle POST request
    else:
        # handle GET request
```

## Form Handling

```python
from flask import request

@app.route('/submit', methods=['POST'])
def submit_form():
    name = request.form['name']
    email = request.form['email']
    return f'Received {name}, {email}'
```

## Redirects and Errors

```python
from flask import redirect, url_for, abort

@app.route('/redirect')
def redirect_example():
    return redirect(url_for('hello'))

@app.route('/error')
def error_example():
    abort(404)
```

## Flask Extensions

- Flask offers several extensions for tasks like form validation, database integration, user authentication, etc.
- Example: Flask-SQLAlchemy for ORM, Flask-WTF for forms.

```bash
pip install flask-sqlalchemy
pip install flask-wtf
```

## Deploying Flask Apps

- Popular platforms for deployment include Heroku, AWS, and GCP.
- Use environment variables for configuration.

