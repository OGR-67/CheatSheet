# My Programming Cheatsheets

- [Bash](#Bash)
- [Git](#Git)
- [RegEx](#RegEx)
- [Python](#Python)
- [Javascript](#Javascript)

# Bash
[Back to summary](#My-Programming-Cheatsheets)  
- [Shortcuts](#Shortcuts)
- [Variables](#Variables)
- [IO Redirection](#IO-Redirection)
- [Command Lists](#Command-Lists)
- [Directory Operations](#Directory-Operations)
- [ls Options](#ls-Options)
- [Search Files](#Search-Files)
- [File Operations](#File-Operations)
- [Watch a Command](#Watch-a-Command)
- [Process Management](#Process-Management)
- [Nano Shortcuts](#Nano-Shortcuts)
- [File Permissions](#File-Permissions)
- [File Permission Numbers](#File-Permission-Numbers)

## Shortcuts
[Back to summary](#Bash)    
```bash
CTRL-c      Stop current command  
CTRL-z      Sleep program  
CTRL-a      Go to start of line  
CTRL-e      Go to end of line  
CTRL-u      Cut from start of line  
CTRL-k      Cut to end of line  
CTRL-r      Search history  
!!          Repeat last command  
!abc        Run last command starting with abc  
!abc:p      Print last command starting with abc  
!$          Last argument of previous command  
ALT-.       Last argument of previous command  
!*          All arguments of previous command  
^abc^123    Run previous command, replacing abc with 123  
$_          Value of inline previous command  
```

## Variables
[Back to summary](#Bash)    
```bash
env                 Show environment variables  
echo $NAME          Output value of $NAME variable  
export NAME=value   Set $NAME to value  
$PATH               Executable search path  
$HOME               Home directory  
$SHELL              Current shell  
```

## IO Redirection
[Back to summary](#Bash)    
```bash
cmd < file        Input of cmd from file  
cmd1 <(cmd2)      Output of cmd2 as file input to cmd1  
cmd > file        Standard output (stdout) of cmd to file  
cmd > /dev/null   Discard stdout of cmd  
cmd >> file       Append stdout to file  
cmd 2> file       Error output (stderr) of cmd to file  
cmd 1>&2          stdout to same place as stderr  
cmd 2>&1          stderr to same place as stdout  
cmd &> file       Every output of cmd to file  
```

## Pipes
[Back to summary](#Bash)    
```bash
cmd1 | cmd2       stdout of cmd1 to cmd2  
cmd1 |& cmd2      stderr of cmd1 to cmd2  
```

## Command Lists
[Back to summary](#Bash)    
```bash
cmd1 ; cmd2     Run cmd1 then cmd2  
cmd1 && cmd2    Run cmd2 if cmd1 is successful  
cmd1 || cmd2    Run cmd2 if cmd1 is not successful  
cmd &           Run cmd in a subshell  
```

## Directory Operations
[Back to summary](#Bash)    
```bash
pwd         Show current directory
mkdir dir   Make directory dir
cd dir      Change directory to dir
cd ..       Go up a directory
ls          List files
```

## ls Options
[Back to summary](#Bash)    
```bash
-a    Show all (including hidden)
-R    Recursive list
-r    Reverse order
-t    Sort by last modified
-S    Sort by file size
-l    Long listing format
-1    One file per line
-m    Comma- separated output
-Q    Quoted output
```

## Search Files
[Back to summary](#Bash)    
```bash
grep pattern files      Search for pattern in files
grep -i                 Case insensitive search
grep -r                 Recursive search
grep -v                 Inverted search
grep -o                 Show matched part of file only
find /dir/ -name name*  Find files starting with name in dir
find /dir/ -user name   Find files owned by name in dir
find /dir/ -mmin num    Find files modifed less than num minutes ago in dir
whereis command         Find binary/source/manual for command
locate file             Find file (quick search of system index)
```
## File Operations
[Back to summary](#Bash)    
```bash
touch file1       Create file1
cat file1 file2   Concatenate files and output
less file1        View and paginate file1
file file1        Get type of file1
cp file1 file2    Copy file1 to file2
mv file1 file2    Move file1 to file2
rm file1          Delete file1
head file1        Show first 10 lines of file1
tail file1        Show last 10 lines of file1
tail -F file1     Output last lines of file1 as it changes
```

## Watch a Command
[Back to summary](#Bash)    
```bash
watch -n 5 'ntpq -p'    Issue the 'ntpq -p' command every 5 seconds and display output
```

## Process Management
[Back to summary](#Bash) 
```bash
ps            Show snapshot of processes
top           Show real time processes
kill pid      Kill process with id pid
pkill name    Kill process with name name
killall name  Kill all processes with names beginning name
```

## Nano Shortcuts
[Back to summary](#Bash) 
Files
```
Ctrl-R    Read file
Ctrl-O    Save file
Ctrl-X    Close file
```
Cut and Paste
```
ALT-A     Start marking text
CTRL-K    Cut marked text or line
CTRL-U    Paste text
```
Navigate File
```
ALT-/     End of file
CTRL-A    Beginning of line
CTRL-E    End of line
CTRL-C    Show line number
CTRL-_    Go to line number
```
Search File
```
CTRL-W    Find
ALT-W     Find next
CTRL-\    Search and replace
```

## File Permissions
[Back to summary](#Bash) 
```bash
Change mode of file to 775
chmod 775 file

Recurs ively chmod folder to 600
chmod -R 600 folder 

Change file owner to user and group to group
chown user:group file
```

## File Permission Numbers
[Back to summary](#Bash)  
First digit is owner permis sion, second is group and third is everyone.
```bash
4   read (r)
2   write (w)
1   execute (x)
```

# Git
[Back to summary](#My-Programming-Cheatsheets)  
- [SETUP](#SETUP)
- [SETUP & INIT](#SETUP-AND-INIT)
- [STAGE & SNAPSHOT](#STAGE-AND-SNAPSHOT)
- [BRANCH & MERGE](#BRANCH-AND-MERGE)
- [INSPECT & COMPARE](#INSPECT-AND-COMPARE)
- [TRACKING PATH CHANGES](#TRACKING-PATH-CHANGES)
- [IGNORING PATTERNS](#IGNORING-PATTERNS)
- [SHARE & UPDATE](#SHARE-AND-UPDATE)
- [REWRITE HISTORY](#REWRITE-HISTORY)
- [TEMPORARY COMMITS](#TEMPORARY-COMMITS)

## SETUP
[Back to summary](#Git)  
  
Set a name that is identifiable for credit when review version history
```bash
git config --global user.name “[firstname lastname]”
```
Set an email address that will be associated with each history marker  
```bash
git config --global user.email “[valid-email]”
```
Set automatic command line coloring for Git for easy reviewing
```bash
git config --global color.ui auto
```

## SETUP AND INIT
[Back to summary](#Git) 
Initialize an existing directory as a Git repository
```bash
git init
```
Retrieve an entire repository from a hosted location via URL
```bash
git clone [url]
```

## STAGE AND SNAPSHOT
[Back to summary](#Git) 
Show modified files in working directory, staged for your next commit
```bash
git status
```
Add a file as it looks now to your next commit (stage)
```bash
git add [file]
```
Unstage a file while retaining the changes in working directory
```bash
git reset [file]
```
Diff of what is changed but not staged
```bash
git diff
```
Diff of what is staged but not yet committed
```bash
git diff --staged
```
Commit your staged content as a new commit snapshot
```bash
git commit -m “[descriptive message]”
```

## BRANCH AND MERGE
[Back to summary](#Git)  
List your branches.  
A * will appear next to the currently active branch
```bash
git branch
```
Rename Master branch to main
```bash
git branch -M main

```
Create a new branch at the current commit
```bash
git branch [branch-name]
```
Switch to another branch and check it out into your working directory
```bash
git checkout
```
Merge the specified branch’s history into the current one
```bash
git merge [branch]
```
Show all commits in the current branch’s history
```bash
git log
```
Visualize log tree
```bash
$ git log --oneline --decorate --graph --all
```

## INSPECT AND COMPARE
[Back to summary](#Git)  
Show the commit history for the currently active branch
```bash
git log
```
Show the commits on branchA that are not on branchB
```bash
git log branchB..branchA
```
Show the commits that changed file, even across renames
```bash
git log --follow [file]
```
Show the diff of what is in branchA that is not in branchB
```bash
git diff branchB...branchA
```
Show any object in Git in human-readable format
```bash
git show [SHA]
```

## TRACKING PATH CHANGES
[Back to summary](#Git)  
Delete the file from project and stage the removal for commit
```bash
git rm [file]
```
Change an existing file path and stage the move
```bash
git mv [existing-path] [new-path]
```
Show all commit logs with indication of any paths that moved
```bash
git log --stat -M
```

## IGNORING PATTERNS
[Back to summary](#Git)  

Save a file with desired patterns as .gitignore with either direct string matches or wildcard globs.
```
logs/
*.notes
pattern*/
```
System wide ignore pattern for all local repositories
```bash
git config --global core.excludesfile [file]
```

## SHARE AND UPDATE
[Back to summary](#Git)  
Add a git URL as an alias
```bash
git remote add [alias] [url]
```
Fetch down all the branches from that Git remote
```bash
git fetch [alias]
```
Merge a remote branch into your current branch to bring it up to date
```bash
git merge [alias]/[branch]
```
Transmit local branch commits to the remote repository branch
```bash
git push [alias] [branch]
```
Fetch and merge any commits from the tracking remote branch
```bash
git pull
```

## REWRITE HISTORY
[Back to summary](#Git)  
Apply any commits of current branch ahead of specified one
```bash
git rebase [branch]
```
Clear staging area, rewrite working tree from specified commit
```bash
git reset --hard [commit]
```

## TEMPORARY COMMITS
[Back to summary](#Git)  
Save modified and staged changes
```bash
git stash
```
List stack-order of stashed file changes
```bash
git stash list
```
Write working from top of stash stack
```bash
git stash pop
```
Discard the changes from top of stash stack
```bash
git stash drop
```

# RegEx
[Back to summary](#My-Programming-Cheatsheets)  
- [Anchors](#Anchors)
- [Character Classes](#Character-Classes)
- [POSIX](#POSIX)
- [Assertions](#Assertions)
- [Quantifiers](#Quantifiers)
- [Escape Sequences](#Escape-Sequences)
- [Common Metacharacters](#Common-Metacharacters)
- [Special Characters](#Special-Characters)
- [Groups and Ranges](#Groups-and-Ranges)
- [Pattern Modifiers](#Pattern-Modifiers)
- [String Replacement](#String-Replacement)

## Anchors
[Back to summary](#RegEx)  
```
^           Start of string, or start of line in multiline pattern
\A          Start of string
$           End of string, or end of line in multi-line pattern
\Z          End of string
\b          Word boundary
\B          Not word boundary
\<          Start of word
\>          End of word
```
## Character Classes
[Back to summary](#RegEx)  
```
\c          Control character
\s          White space
\S          Not white space
\d          Digit
\D          Not digit
\w          Word
\W          Not word
\x          Hexadecimal digit
\O          Octal digit
```
## POSIX
[Back to summary](#RegEx)  
```
[:upper:]   Uppercase letters
[:lower:]   Lowercase letters
[:alpha:]   All letters
[:alnum:]   Digits and letters
[:digit:]   Digits
[:xdigit:]  Hexadecimal digits
[:punct:]   Punctu ation
[:blank:]   Space and tab
[:space:]   Blank characters
[:cntrl:]   Control characters
[:graph:]   Printed characters
[:print:]   Printed characters and spaces
[:word:]    Digits, letters and underscore
```
## Assertions
[Back to summary](#RegEx)  
```
?=          Lookahead assertion
?!          Negative lookahead
?<=         Lookbehind assertion
?!= or ?<!  Negative lookbehind
?>          Once-only Subexp ression
?()         Condition [if then]
?()|        Condition [if then else]
?#          Comment
```
## Quantifiers
[Back to summary](#RegEx)  
```
*           0 or more 
+           1 or more 
?           0 or 1 
{3}         Exactly 3
{3,}        3 or more
{3,5}       3, 4 or 5
```
## Escape Sequences
[Back to summary](#RegEx)  
```
\           Escape following character
\Q          Begin literal sequence
\E          End literal sequence
```
## Common Metacharacters
[Back to summary](#RegEx)  
```
^   [   .   $
{   *   (   \
+   )   |   ?
<   >
```
## Special Characters
[Back to summary](#RegEx)  
```
\n          New line
\r          Carriage return
\t          Tab
\v          Vertical tab
\f          Form feed
\xxx        Octal character xxx
\xhh        Hex character hh
```
## Groups and Ranges
[Back to summary](#RegEx)  
```
.           Any character except new line (\n)
(a|b)       a or b
(...)       Group
(?:...)     Passive (non-c apt uring) group
[abc]       Range (a or b or c)
[^abc]      Not (a or b or c)
[a-q]       Lower case letter from a to q
[A-Q]       Upper case letter from A to Q
[0-7]       Digit from 0 to 7
\x          Group/ sub pattern number " x"
```
## Pattern Modifiers
[Back to summary](#RegEx)  
```
g           Global match
i *         Case-insensitive
m *         Multiple lines
s *         Treat string as single line
x *         Allow comments and whitespace in pattern
e *         Evaluate replacement
U *         Ungreedy pattern
```

## String Replacement
[Back to summary](#RegEx)  
```
$n          nth non-passive group
$2          "xyz" in /^(abc (xy z))$/
$1          "xyz" in /^(?:a bc) (xyz)$/
$`          Before matched string
$'          After matched string
$+          Last matched string
$&          Entire matched string
```

# Python
[Back to summary](#My-Programming-Cheatsheets)  
- [Django](#Django)


# Django
[Back to summary](#My-Programming-Cheatsheets)  
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
[back to summary](#Django)  
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
[back to summary](#Django)  
This will create a mysite directory in your current directory the manage.py file
```bash
django-admin startproject mysite (or I like to call it config)
```

You can check that everything went fine
```bash
python manage.py runserver
```

## Database Setup
[back to summary](#Django)  
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
[back to summary](#Django)  
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
[back to summary](#Django)  
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
[back to summary](#Django)  
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
[back to summary](#Django)  
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
[back to summary](#Django)  
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
[back to summary](#Django)  
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
[back to summary](#Django)  
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
[back to summary](#Django)  
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

## Render Form In Template
[back to summary](#Django)  
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
[back to summary](#Django)  
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
[back to summary](#Django)  
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

## Allow Users to Own Their Data
[back to summary](#Django)  
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
[back to summary](#Django)  
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
[back to summary](#Django)  
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
--- Work In Progress --

# Javascript
[Back to summary](#My-Programming-Cheatsheets)  
- [Working With Array](#Working-With-Array)
- [Working With Strings](#Working-With-Strings)
- [Working With Objects](#Working-With-Objects)
- [Node JS](#nodeJS)
- [ExpressJS](#expressJS)
- [EJS](#EJS)

## Working With Array
[Back to summary](#Javascript) 
### reduce()  
The reduce() method executes a user-supplied "reducer" callback function on each element of the array, in order, passing in the return value from the calculation on the preceding element. The final result of running the reducer across all elements of the array is a single value.

```javascript
function find_average(array) {
//   a is accumulator and b is current value being processed
//   0 is the initial value of the accumulator
  return array.reduce(function(a,b){
      a + b
    }, 0) / array.length;
}
```
### reverse()
The reverse() method reverses an array in place. The first array element becomes the last, and the last array element becomes the first.
```javascript
const array1 = ['one', 'two', 'three'];
console.log('array1:', array1);
// expected output: "array1:" Array ["one", "two", "three"]

// Careful: reverse is destructive -- it changes the original array.
console.log('array1:', array1);
// expected output: "array1:" Array ["three", "two", "one"]
```
### join()
The join() method creates and returns a new string by concatenating all of the elements in an array (or an array-like object), separated by commas or a specified separator string. If the array has only one item, then that item will be returned without using the separator.
```javascript
console.log(elements.join());
// expected output: "Fire,Air,Water"

console.log(elements.join(''));
// expected output: "FireAirWater"

console.log(elements.join('-'));
// expected output: "Fire-Air-Water"
```
### map()
The map() method creates a new array populated with the results of calling a provided function on every element in the calling array.
```javascript
// Arrow function
map((element) => { /* ... */ })
map((element, index) => { /* ... */ })
map((element, index, array) => { /* ... */ })

// Callback function
map(callbackFn)
map(callbackFn, thisArg)

// Inline callback function
map(function(element) { /* ... */ })
map(function(element, index) { /* ... */ })
map(function(element, index, array){ /* ... */ })
map(function(element, index, array) { /* ... */ }, thisArg)
```

## Working With Strings
[Back to summary](#Javascript) 
### split()
The split() method divides a String into an ordered list of substrings, puts these substrings into an array, and returns the array.
```javascript
const str = 'The quick brown fox jumps over the lazy dog.';

const words = str.split(' ');
console.log(words[3]);
// expected output: "fox"

const chars = str.split('');
console.log(chars[8]);
// expected output: "k"

const strCopy = str.split();
console.log(strCopy);
// expected output: Array ["The quick brown fox jumps over the lazy dog."]

```
### substring()
The substring() method returns the part of the string between the start and end indexes, or to the end of the string.
```javascript
const str = 'Google';

console.log(str.substring(1, 3));
// expected output: "oo"
```

## Working With Objects
[Back to summary](#Javascript) 
### 3 ways to loop through objects
Get an Array of keys
```javascript
const courses = {
    java: 10,
    javascript: 55,
    nodejs: 5,
    php: 15
};

const keys = Object.keys(courses);
// [ 'java', 'javascript', 'nodejs', 'php' ]
```
Get an Array of values
```javascript
const animals = {
    tiger: 1,
    cat: 2,
    monkey: 3,
    elephant: 4
};
Object.values(animals)
// [1, 2, 3, 4]
```
Get an Array of [Key / Value] pairs
```javascript
const animals = {
    tiger: 1,
    cat: 2,
    monkey: 3,
    elephant: 4
};

Object.entries(animals)
//[[ 'tiger', 1 ], [ 'cat', 2 ], [ 'monkey', 3 ], [ 'elephant', 4 ]]
```


## nodeJS
[Back to summary](#Javascript) 
Init node to create package.json
```bash
node init
```
Install packages inside your project
```bash
npm install package_name
```
Install packages to your system
```bash
npm install -g package_name
```

## expressJS
[Back to summary](#Javascript) 
Install express
```bash
npm install express --save
```
Install body-parser
```bash
npm i body-parser
```
Install ejs
```bash
npm install ejs
```
Web app boiler plate
```javascript
const express = require("express");
const bodyParser = require("body-parser");
const ejs = require("ejs");

// #### App settup ####
const app = express();
app.set("view engine", "ejs"); // Tell express to use ejs rendering engine

app.use(bodyParser.urlencoded({ extended: true }));
app.use(express.static("public")); // Serves statics files in root/public folder

// #### Routes ####
// Home
app.get("/", (req, res) => {
  res.render(__dirname + "/views/home.ejs", context);
});


// #### Port Listening ####
app.listen(3000, function () {
  console.log("Server started on port 3000");
});

```
## EJS
[Back to summary](#Javascript) 
### Tags
Use inside .ejs templates
```
# Script
<% 'Scriptlet' tag, for control-flow, no output
<%_ ‘Whitespace Slurping’ Scriptlet tag, strips all whitespace before it

# Variable
<%= Outputs the value into the template (HTML escaped)
<%- Outputs the unescaped value into the template

# Comment
<%# Comment tag, no execution, no output

# Litteral
<%% Outputs a literal '<%'

# Ending tags
%> Plain ending tag
-%> Trim-mode ('newline slurp') tag, trims following newline
_%> ‘Whitespace Slurping’ ending tag, removes all whitespace after it

```
### Includes
Includes are relative to the template with the include call. (This requires the 'filename' option.) For example if you have "./views/users.ejs" and "./views/user/show.ejs" you would use <%- include('user/show'); %>.

You'll likely want to use the raw output tag (<%-) with your include to avoid double-escaping the HTML output.
```html
<ul>
  <% users.forEach(function(user){ %>
    <%- include('user/show', {user: user}); %>
  <% }); %>
</ul>
```

--- Work In Progress ---
