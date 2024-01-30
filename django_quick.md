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
  - `__init__.py`: Makes the directory a Python package
  - `settings.py`: Configuration settings
  - `urls.py`: URL declarations
  - `wsgi.py`: Entry-point for WSGI web servers
- `myapp/`: Application directory
  - `migrations/`: Database migrations
  - `models.py`: Database models
  - `views.py`: Request/response logic
  - `admin.py`: Admin interface config
  - `apps.py`: App configuration
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
- Django template language

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

## Creating REST API

1. Install Django REST Framework:
   ```bash
   pip install djangorestframework
   ```

2. Add `'rest_framework'` to `INSTALLED_APPS` in `settings.py`.

3. Create a serializer in `serializers.py`:
   ```python
   from rest_framework import serializers
   from .models import MyModel

   class MyModelSerializer(serializers.ModelSerializer):
       class Meta:
           model = MyModel
           fields = ['id', 'name', 'description', 'created_at']
   ```

4. Create a viewset in `views.py`:
   ```python
   from rest_framework import viewsets
   from .models import MyModel
   from .serializers import MyModelSerializer

   class MyModelViewSet(viewsets.ModelViewSet):
       queryset = MyModel.objects.all()
       serializer_class = MyModelSerializer
   ```

5. Update `urls.py` to include the REST API routes:
   ```python
   from rest_framework.routers import DefaultRouter
   from .views import MyModelViewSet

   router = DefaultRouter()
   router.register(r'mymodel', MyModelViewSet)

   urlpatterns += router.urls
   ```

## Creating Superuser

```bash
# Create a superuser for the admin panel
python manage.py createsuperuser
```

- Follow the prompts to set the username, email, and password.

## Authentication

1. Use Django's built-in authentication system:
   - Update `settings.py`:
     ```python
     AUTHENTICATION_BACKENDS = [
         'django.contrib.auth.backends.ModelBackend',
     ]
     ```

2. Create login and logout views:
   - Use `django.contrib.auth.views` for standard authentication views.
   - Define `LOGIN_REDIRECT_URL` and `LOGOUT_REDIRECT_URL` in `settings.py`.

3. Secure views with `@login_required` decorator:
   ```python
   from django.contrib.auth.decorators import login_required

   @login_required
   def my_secure_view(request):
       # Your view logic here
   ```

4. Update `urls.py` to include authentication URLs:
   ```python
   from django.contrib.auth import views as auth_views

   urlpatterns = [
       path

    ('login/', auth_views.LoginView.as_view(), name='login'),
           path('logout/', auth_views.LogoutView.as_view(), name='logout'),
           # Other URLs...
       ]
   ```

## Types of Views in Django

Django supports several types of views:

1. **Function-Based Views (FBVs):** Simple and straightforward, defined as regular Python functions. Example:
    ```python
    from django.http import HttpResponse

    def my_view(request):
        return HttpResponse('Hello, World!')
    ```

2. **Class-Based Views (CBVs):** More reusable and modular, organized as classes. Example:
    ```python
    from django.views import View
    from django.http import HttpResponse

    class MyView(View):
        def get(self, request):
            return HttpResponse('Hello, World!')
    ```

3. **Generic Views:** Built-in views provided by Django for common use cases like displaying a list of objects or a detail page for an object. Example:
    ```python
    from django.views.generic import ListView
    from .models import MyModel

    class MyListView(ListView):
        model = MyModel
    ```

4. **Template Views:** Render a specific template. Example:
    ```python
    from django.views.generic import TemplateView

    class MyTemplateView(TemplateView):
        template_name = "my_template.html"
    ```

5. **Form Views:** Manage forms, including displaying and processing them. Example:
    ```python
    from django.views.generic.edit import FormView
    from .forms import MyForm

    class MyFormView(FormView):
        form_class = MyForm
        template_name = 'my_form.html'
    ```

6. **REST Framework Views:** For creating API endpoints (if using Django REST Framework). Example:
    ```python
    from rest_framework.views import APIView
    from rest_framework.response import Response

    class MyAPIView(APIView):
        def get(self, request):
            return Response({"message": "Hello, World!"})
    ```

 ### ORM Queries in Django

#Django's ORM (Object-Relational Mapping) allows you to interact with the database using Python code instead of writing raw SQL queries. Here's how different ORM queries work:

1. **Retrieving All Records:**
    ```python
    all_items = MyModel.objects.all()
    ```

2. **Filtering Records:**
    ```python
    filtered_items = MyModel.objects.filter(name="example")
    ```

3. **Getting a Single Record:**
    ```python
    single_item = MyModel.objects.get(id=1)
    ```

4. **Creating a New Record:**
    ```python
    new_item = MyModel.objects.create(name="New Item")
    ```

5. **Updating Records:**
    ```python
    MyModel.objects.filter(name="example").update(description="New Description")
    ```

6. **Deleting Records:**
    ```python
    MyModel.objects.filter(name="example").delete()
    ```

7. **Chaining QuerySets:**
    You can chain query methods to combine filters.
    ```python
    items = MyModel.objects.filter(name="example").exclude(description="Old")
    ```

8. **Aggregations:**
    Performing calculations on a set of values.
    ```python
    from django.db.models import Avg
    average = MyModel.objects.all().aggregate(Avg("some_field"))
    ```

9. **Complex Queries (Q Objects):**
    For complex query conditions.
    ```python
    from django.db.models import Q
    complex_query = MyModel.objects.filter(Q(name="example") | Q(description="detailed"))
    ```

10. **Raw SQL Queries:**
    Executing raw SQL queries if needed.
    ```python
    raw_query = MyModel.objects.raw('SELECT * FROM myapp_mymodel WHERE name = %s', ['example'])
    ```

These ORM techniques in Django make data manipulation more intuitive and reduce the risk of SQL injection attacks, as Django ORM takes care of properly escaping queries.


## Variations of Viewsets

### ModelViewSet
- For full CRUD operations.
- Automatically provides `list`, `create`, `retrieve`, `update`, and `delete` actions.
```python
from rest_framework import viewsets
from .models import MyModel
from .serializers import MyModelSerializer

class MyModelViewSet(viewsets.ModelViewSet):
    queryset = MyModel.objects.all()
    serializer_class = MyModelSerializer
```

### ReadOnlyModelViewSet
- Provides read-only access (list and detail views).
```python
class MyReadOnlyModelViewSet(viewsets.ReadOnlyModelViewSet):
    queryset = MyModel.objects.all()
    serializer_class = MyModelSerializer
```

### GenericViewSet
- Customizable behavior using mixins.
- Can be used to create custom viewsets.
```python
from rest_framework import mixins, viewsets

class MyCustomViewSet(mixins.ListModelMixin, 
                      mixins.RetrieveModelMixin,
                      viewsets.GenericViewSet):
    queryset = MyModel.objects.all()
    serializer_class = MyModelSerializer
```

## Serializers

### ModelSerializer
- Simplifies serialization for model instances.
```python
from rest_framework import serializers

class MyModelSerializer(serializers.ModelSerializer):
    class Meta:
        model = MyModel
        fields = ['id', 'name', 'description']
```

### HyperlinkedModelSerializer
- Similar to ModelSerializer but uses hyperlinks.
```python
class MyModelHyperlinkedSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = MyModel
        fields = ['url', 'name', 'description']
```

### Serializer
- Base class for custom serializers.
```python
class MyCustomSerializer(serializers.Serializer):
    name = serializers.CharField(max_length=100)
    description = serializers.CharField()
```

## Middleware

### Creating Custom Middleware
- Custom middleware for logging requests.
```python
class LogMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        response = self.get_response(request)
        # Custom logging logic here
        return response
```

### Common Uses
- Middleware for authentication, logging, modifying request/response.

## Settings

### Database Configuration
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```

### Installed Apps
```python
INSTALLED_APPS = [
    'myapp.apps.MyAppConfig',
    'django.contrib.admin',
    # ...
]
```

### Middleware Configuration
```python
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    # ...
]
```

### Template Settings
```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        # ...
    },
]
```

### Static and Media Files Management
```python
STATIC_URL = '/static/'
MEDIA_URL = '/media/'
```

## Django REST Framework Configuration

### Pagination
```python
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10
}
```

### Permissions
```python
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ]
}
```

### Authentication Classes
```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.BasicAuthentication',
        'rest_framework.authentication.SessionAuthentication',
    ]
}
```

### Throttling
```python
REST_FRAMEWORK = {
    'DEFAULT_THROTTLE_CLASSES': [
        'rest_framework.throttling.UserRateThrottle'
    ],
    'DEFAULT_THROTTLE_RATES': {
        'user': '1000/day'
    }
}
```

## Django Forms

### Form Classes
- Creating a form from a model.
```python
from django import forms
from .models import MyModel

class MyModelForm(forms.ModelForm):
    class Meta:
        model = MyModel
        fields = ['name', 'description']
```

### Form Validation
- Custom validation methods for forms.
```python
class MyModelForm(forms.ModelForm):
    class Meta:
        model = MyModel
        fields = ['name', 'description']

    def clean_name(self):
        name = self.cleaned_data['name']
        # Custom validation logic
        return name
```

### Rendering Forms
- Displaying forms in templates.
```html
<!-- In template -->
<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Submit</button>
</form>
```

## Testing in Django

### Unit Tests
- Testing individual units of code.
```python
from django.test import TestCase
from .models import MyModel

class MyModelTest(TestCase):
