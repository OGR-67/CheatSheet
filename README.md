# My Programming Cheatsheets

- [Python](#Python)
- [Javascript](#Javascript)

# Python
# Django
- [Preparing Environnement](#Preparing%20Environnement)
- [Create project](#Create%20project)
- [Database Setup](#Database-Setup)
- [Creating an app](#Creating-an-app)
- [Creating models](#Creating-models)
- [Database editing](#Database-editing)
- [Administration](#Administration)
- [Management](#Management)
- [Views](#Views)

## Preparing Environnement

Create project folder and navigate to it
```bash
mkdir project_name && cd $_
```
Create venv for the project
```bash
python -m venv env_name
```
Activate environnement (Replace "bin" by "Scripts" in Windows)
```bash
source env_name\bin\activate
```
Install Django (and others dependencies if needed)
```bash
pip install django
```
Create requirements file
```bash
pip freeze > requirements.txt
```
Use this commmand to nstall all required files based on your pip freeze command
```bash
pip install -r requirements.txt
```
Version control initialisation, be sure to create appropriate gitignore
```bash
git init
```

## Create project

This will create a mysite directory in your current directory the manage.py file
```bash
django-admin startproject mysite (or I like to call it config)
```

You can check that everything went fine
```bash
python manage.py runserver
```

## Database Setup
Open up mysite/settings.py. It’s a normal Python module with module-level variables representing Django settings.  
If you wish to use another database, install the appropriate database bindings and change the following keys in the DATABASES 'default' item to match your database connection settings
```python
ENGINE – 'django.db.backends.sqlite3', 'django.db.backends.postgresql', 'django.db.backends.mysql', or 'django.db.backends.oracle'
```

The default value, BASE_DIR / 'db.sqlite3', will store the file in your project directory  
NAME – The name of your database. If you’re using SQLite, the database will be a file on your computer; in that case, NAME should be the full absolute path, including filename, of that file.  
The default value, BASE_DIR / 'db.sqlite3', will store the file in your project directory.  
If you are not using SQLite as your database, additional settings such as USER, PASSWORD, and HOST must be added.  
For more details, see the reference documentation for [DATABASES](https://docs.djangoproject.com/en/4.0/ref/settings/#std:setting-DATABASES).  

## Creating an app
Create an app_name directory and all default file/folder inside
```bash
python manage.py startapp app_name
```
Apps are "plugable",  "plug in" the app into the project by adding it in installed apps in settings.py
```python
INSTALLED_APPS = [
 'app_name',
 ...
```
Into urls.py from project folder, inculde app urls to project
```python
urlpatterns = [
 path('app_name/', include('app_name.urls')),
 path('admin/', admin.site.urls),
]
```

## Creating models
Create your class in the app_name/models.py file and add [fields](https://docs.djangoproject.com/en/3.2/ref/models/fields/).  
It’s important to add __str__() methods to your models, because objects’ representations are used throughout Django’s automatically-generated admin.
```python
from django.db import models

Class ModelName(models.Model):
  """A very basic model"""
  title = models.CharField(max_length=100) #max-length is required with charfiel
  
  def __str__(self):
    return self.title
```

## Database editing
By running makemigrations, you’re telling Django that you’ve made some changes to your models
you can specify app_name or not
```bash
python manage.py makemigrations (app_name)
```
Check the SQL commands that migration would run (identifier is given with makemigrations command).
```bash
python manage.py sqlmigrate #identifier
```
Check for any problems in your project without migrate database
```bash
python manage.py check
```
Create tables and fields in database based on your models
```bash
python manage.py migrate
```
Hop into the interactive Python shell and play around with the free API Django gives you
```bash
python manage.py shell
```

## Administration
Create a user who can login to the admin site
```bash
python manage.py createsuperuser
```
Into app_name/admin.py, add the model to administration site
```python
from django.contrib import admin
from .models import ModelName

admin.site.register(ModelName)
```
Open a web browser and go to “/admin/” on your local domain

## Management
Django allows you to create customs CLI commands.  
First, create required folders
```bash
mkdir app_name/management app_name/management/commands && cd $_
```
Create a python file with your command name
```bash
touch your_command_name.py
```
Edit your new python file. Create a class that will handle your command.
```python
from django.core.management.base import BaseCommand
# import anything else you need to work with (models?)

class Command(BaseCommand):
  help = "This message will be shown with the --help option after your command"

  def handle(self, args, *kwargs):
   # Task the command is supposed to do
```
You can now execute your command
```bash
python manage.py my_custom_command
```

## Views

Open the file app_name/views.py and put the following Python code in it.
This is the simplest view possible.
```python
from django.http import HttpResponse

def index(request):
 return HttpResponse("Hello, world. You're at the index.")
```
In the app_name/urls.py file include the following code.  
This will specif the routes of your app
```python
from django.urls import path
from . import views

app_name = "app_name"
urlpatterns = [
 path('', views.index, name='index'),
]
```
You can pass arguments to your views like in the exemple below.  
```python
def detail(request, question_id):
 return HttpResponse(f"You're looking at question {question_id}")
```
And this is how you pass arguments in url
```python
urlpatterns = [
 path('<int:question_id>/', views.detail, name='detail'),
 ...
```
Finaly, we can pass arguments to template like this
```
{% url 'app_name:view_name' question_id %}
```
This is the folder path to follow for template
```bash
app_name/templates/app_name/index.html
```
Pass values from views to template.  
We use the render shortcut here
```python
def index(request):
    page_title = "Randomecipe - Home Page"
    context = {"page_title": page_title}
    return render(request, "app_name/index.html", context)
```
Get a look at Django's [documentation](https://docs.djangoproject.com/en/4.0/topics/templates/) to see how you can edit templates.

## Javascript
