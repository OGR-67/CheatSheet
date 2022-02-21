# My Programming Cheatsheets

- [Python](#Python)
- [Javascript](#Javascript)

# Python
# Django
- [Preparing Environnement](#Preparing-Environnement)
- [Create project](#Create-project)
- [Database Setup](#Database-Setup)
- [Creating an app](#Creating-an-app)
- [Creating models](#Creating-models)
- [Database editing](#Database-editing)
- [Administration](#Administration)
- [Management](#Management)
- [Views](#Views)
- [Add some static files](#Add-some-static-files)
- [Render Form In Template](#Render-Form-In-Template)
- [Custom template tags and filters](#Custom-template-tags-and-filters)
- [Setting Up User Accounts](#Setting-Up-User-Accounts)
- [Allow Users to Own Their Data](#Allow-Users-to-Own-Their-Data)
- [Paginator](#Paginator)
- [Deploy to Heroku](#Deploy-to-Heroku)

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
Redirect to 404 page if nothing is found
```python
question = get_object_or_404(Question, pk=question_id)
```

Get a look at Django's [documentation](https://docs.djangoproject.com/en/4.0/topics/templates/) to see how you can edit templates.

## Add some static files

Be sure to have this in your INSTALLED_APPS
```python
'django.contrib.staticfiles'
```
Create static folder associated with your app
```bash
mkdir app_name/static app_name/static/app_name
```
Put this on top of your template
```html
{% load static %}
```
Exemple of use static for stylesheet
```html
<link rel="stylesheet" type="text/css" href="{% static 'app_name/style.css' %}">
```

## Forms
Create form module
```bash
touch app_name/forms.py
```
An exemple of form with Form inherit 
```python
from django import forms
from .models import YourModel

class ExempleForm(forms.Form):
  exemple_field = forms.CharField(label='Exemple label', max_length=100)
```

An exemple of form with ModelForm inherit  
A ModelForm maps a model class’s fields to HTML form <in­put> elements via a Form. Widget is optional. Use it to override default widget  
Widget [list](https://docs.djangoproject.com/en/3.2/ref/forms/widgets/)
```python
from django import forms
from .models import YourModel

class ExempleForm(forms.ModelForm):
 class meta:
  model = YourModel
  fields = ["fields"]
  labels = {"text": "label_text"}
  widget = {"text": forms.widget_name}
```
In your views, create a blank form if no data submitted
```python
if request.method != "POST":
  form = ExempleForm()
```
The form object contain's the informations submitted by the user
```python
form = ExempleForm(data=request.POST)
```
Form validation. Always use redirect function
```python
is form.isvalid()
  form.save()
  return redirect("app_name:view_name", argument=ardument)
```
In your template, add this tag to prevent "cross-site request forgery" attack
```html
{% csrf_token %}
```

# Render Form In Template
The most simple way to render the form, but usualy it's ugly
```html
{{ form.as_p }}
```
The | is a filter, and here for placeholder, it's a custom one. See next section to see how to create it
```html
{{ field|placeholder:field.label }} 
{{ form.username|placeholder:"Your name here"}}
```
You can extract each fields with a for loop. 
```html
{% for field in form %} 
```
Or by explicitly specifying the field
```html
{{form.username}}
```

## Custom template tags and filters
Django allows you to create customs filter for your templates
Create this folder and this file. Leave it blank.
```bash
touch app_name\templatetags\__init__.py
```
Create a python file with the name of the filter
```bash
app_name\templatetags\filter_name.py
```
Add this on top of your template
```html
{% load filter_name %}
```
To be a valid tag library, the module must contain a module-level variable named register 
that is a template.Library instance.  
Here is an exemple of filter definition.  
See the decorator? It registers your filter with your Library instance.  
You need to restart server for this to take effects.  
```python
from django import template 

register = template.Library()

@register.filter(name='cut') 
def cut(value, arg): 
   """Removes all values of arg from the given string""" 
   return value.replace(arg, '')
```
Here is a link of how to make a [placeholder](https://tech.serhatteker.com/post/2021-06/placeholder-templatetags/) custom template tag which i found essential

## Setting Up User Accounts
Create a "users" app. Don't forget to add app to settings.py and include the URLs from users.  
Inside users/urls.py, add this code to include some default authentification URLs that Django has defined.
```python
app_name = "users"
urlpatterns[
  # include default auth urls.
  path("", include("django.contribe.auth.urls"))
]
```
Basic login.html template  
Save it at save template as users/templates/registration/login.html  
```html
{% if form.error %}
  <p>Your username and password didn't match</p>
{% endif %}
<form method="post" action="{% url 'users:login' %}">
  {% csrf_token %}
  {{ form.as_p }}

  <button name="submit">Log in</button>
  <input type="hidden" name="next" value=" {% url 'app_name:index' %}" />
</form>
```
We can access to it by using
```html
<a href="{% url 'users:login' %}">Log in</a>
```
To check if user is logged in
```html
{% if user.is_authenticated %}
```
Link to logout page, and log out the user.  
Save template as users/templates/registration/logged_out.html
```html
{% url "users:logout" %}
```
Inside users/urls.py, add path to register
```python
path("register/", views.register, name="register"),
```
We write our own register() view inside users/views.py.  
For that we use UserCreationForm, a django building model.  
If method is not post, we render a blank form.  
Else, is the form pass the validity check, an user is created.  
We just have to create a registration.html template in same folder as the login and logged_out.
```python
from django.shortcuts import render, redirect
from django.contrib.auth import login
from django.contrib.forms import UserCreationForm

def register(request):
  if request.method != "POST":
    form = UserCreationForm()
  else:
    form = UserCreationForm(data=request.POST)

    if form.is_valid():
      new_user = form.save()
      login(request, new_user)
      return redirect("app_name:index")

  context = {"form": form}
  return render(request, "registration/register.html", context)
```

# Allow Users to Own Their Data
Restrict access with @login_required decorator
```python
...
from django.contrib.auth.decorators import login_required
...

@login_required
def my_view(request)
  ...
```
If user is not logged in, they will be redirect to the login page.  
To make this work, you need to modify settings.py so Django knows where to find the login page.  
Add the following at the very end.  
```python
# My settings
LOGIN_URL = "users:login"
```
Add this field to your models to connect data to certain users.  
When migrating, you will be prompt to select a default value.  
```python
...
from django.contrib.auth.models import User
...
owner = models.ForeignKey(User, on_delete=models.CASCADE)
```
Use this kind of code in your views to filter data of a specific user
request.user only exist when user is logged in.
```python
user_data = ExempleModel.objects.filter(owner=request.user)
```
Make sure the data belongs to the current user.  
If not the case, raise a 404.
```python
...
from django.http import Http404
...

...
if exemple_data.owner != request.user:
  raise Http404
```
Don't forget to associate user to your data in corresponding views
The "commit=false" attribute let us do that
```python
new_data = form.save(commit=false)
new_data.owner = request.user
new_data.save()
```

## Paginator
In app_name/views.py, import Paginator.
```python
from django.core.paginator import Paginator
```
Then, in your view, Get a list of data.
```python
exemple_list = Exemple.objects.all()
```
Set appropriate pagination
```python
paginator = Paginator(exemple_list, 5) # Show 5 items per page.
```
Get actual page number
```python
page_number = request.GET.get('page')
```
Create your Page Object, and put it in the context
```python
page_obj = paginator.get_page(page_number)
context = {
  "page_obj": page_obj,
  ...
```
The Page Object acts now like your list of data
```html
{% for item in page_obj %}
```
An exemple of what to put on the bottom of your page to navigate through Page Objects
```html
<div class="pagination">
  <span class="step-links">
  {% if page_obj.has_previous %}
    <a href="?page=1">&laquo; first</a>
    <a href="?page={{ page_obj.previous_page_number }}">previous</a>
  {% endif %}
    <span class="current"> Page {{ page_obj.number }} of {{ page_obj.paginator.num_pages }}. </span>
  {% if page_obj.has_next %} 
   <a href="?page={{ page_obj.next_page_number }}">next</a> 
   <a href="?page={{ page_obj.paginator.num_pages }}">last &raquo;</a> 
   {% endif %} 
   </span> 
</div>
```
## Deploy to Heroku
Make a [Heroku](https://heroku.com) account.  
Install Heroku [CLI](https://devcenter.heroku.com:articles/heroku-cli/).  
Install these packages
```bash
pip install psycog2 django-heroku gunicorn
```
updtate requirements.txt
```bash
pip freeze -> requirements.txt
```
At the very end of settings.py, make an Heroku ettings section.  
import django_heroku and tell django to apply django heroku settings.  
The staticfiles to false is not a viable option in production, check whitenoise for that IMO.  
```python
# Heroku settings.
import django_heroku
django_heroku.settings(locals(), staticfiles=False)
if os.environ.get('DEBUG') == "TRUE":
  DEBUG = True
  elif os.environ.get('DEBUG') == "FALSE":
  DEBUG = False
```
--Work In Progress --

## Javascript
