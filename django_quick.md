
# Django Cheat Sheet

## Setup and Installation

```bash
# Install Django
pip install django

# Create a new Django project
django-admin startproject myproject

# Start a new app in the project
python manage.py startapp myapp
```

## Project Structure

- `myproject/`: Root directory of your project
  - `__init__.py`: Tells Python that this directory should be considered a Python package
  - `settings.py`: Configuration settings for the project
  - `urls.py`: URL declarations for the project
  - `wsgi.py`: Entry-point for WSGI-compatible web servers to serve your project
- `myapp/`: Application directory
  - `migrations/`: Contains database migrations
  - `models.py`: Defines your database models
  - `views.py`: Handles the request/response logic
  - `admin.py`: Configuration for the admin interface
  - `apps.py`: Configuration for the app
  - `tests.py`: Test definitions

## Models

```python
from django.db import models

class MyModel(models.Model):
    name = models.CharField(max_length=100)
    description = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.name
```

## Views

```python
from django.shortcuts import render
from .models import MyModel

def my_view(request):
    items = MyModel.objects.all()
    return render(request, 'my_template.html', {'items': items})
```

## Templates

- Located in `myapp/templates/`
- Use Django template language

```html
<!-- my_template.html -->
<html>
<head><title>My App</title></head>
<body>
    <h1>Items</h1>
    <ul>
        {% for item in items %}
            <li>{{ item.name }}</li>
        {% endfor %}
    </ul>
</body>
</html>
```

## URLs

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.my_view, name='my_view'),
]
```

## Migrations

```bash
# Make migrations
python manage.py makemigrations

# Apply migrations
python manage.py migrate
```

## Admin Interface

```python
from django.contrib import admin
from .models import MyModel

admin.site.register(MyModel)
```

## Running the Server

```bash
# Run the development server
python manage.py runserver
```

## Testing

```python
from django.test import TestCase
from .models import MyModel

class MyModelTestCase(TestCase):
    def setUp(self):
        MyModel.objects.create(name="Test")

    def test_model_str(self):
        item = MyModel.objects.get(name="Test")
        self.assertEqual(str(item), "Test")
```

