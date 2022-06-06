# My Programming Cheatsheets

- [Shell](#Shell)
- [Git](#Git)
- [RegEx](#RegEx)
- [Python](#Python)
- [Javascript](#Javascript)
- [MongoDB](#MongoDB)

# Shell
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
```
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
```shell
env                 Show environment variables  
echo $NAME          Output value of $NAME variable  
export NAME=value   Set $NAME to value  
$PATH               Executable search path  
$HOME               Home directory  
$SHELL              Current shell  
```

## IO Redirection
[Back to summary](#Bash)    
```shell
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
```shell
cmd1 | cmd2       stdout of cmd1 to cmd2  
cmd1 |& cmd2      stderr of cmd1 to cmd2  
```

## Command Lists
[Back to summary](#Bash)    
```shell
cmd1 ; cmd2     Run cmd1 then cmd2  
cmd1 && cmd2    Run cmd2 if cmd1 is successful  
cmd1 || cmd2    Run cmd2 if cmd1 is not successful  
cmd &           Run cmd in a subshell  
```

## Directory Operations
[Back to summary](#Bash)    
```shell
pwd         Show current directory
mkdir dir   Make directory dir
cd dir      Change directory to dir
cd ..       Go up a directory
ls          List files
```

## ls Options
[Back to summary](#Bash)    
```shell
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
```shell
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
```shell
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
```shell
watch -n 5 'ntpq -p'    Issue the 'ntpq -p' command every 5 seconds and display output
```

## Process Management
[Back to summary](#Bash) 
```shell
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
Change mode of file to 775
```shell
chmod 775 file
```
Recurs ively chmod folder to 600
```shell
chmod -R 600 folder 
```
Change file owner to user and group to group
```shell
chown user:group file
```

## File Permission Numbers
[Back to summary](#Bash)  
First digit is owner permis sion, second is group and third is everyone.
```shell
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
```shell
git config --global user.name “[firstname lastname]”
```
Set an email address that will be associated with each history marker  
```shell
git config --global user.email “[valid-email]”
```
Set automatic command line coloring for Git for easy reviewing
```shell
git config --global color.ui auto
```

## SETUP AND INIT
[Back to summary](#Git) 
Initialize an existing directory as a Git repository
```shell
git init
```
Retrieve an entire repository from a hosted location via URL
```shell
git clone [url]
```

## STAGE AND SNAPSHOT
[Back to summary](#Git) 
Show modified files in working directory, staged for your next commit
```shell
git status
```
Add a file as it looks now to your next commit (stage)
```shell
git add [file]
```
Unstage a file while retaining the changes in working directory
```shell
git reset [file]
```
Diff of what is changed but not staged
```shell
git diff
```
Diff of what is staged but not yet committed
```shell
git diff --staged
```
Commit your staged content as a new commit snapshot
```shell
git commit -m “[descriptive message]”
```

## BRANCH AND MERGE
[Back to summary](#Git)  
List your branches.  
A * will appear next to the currently active branch
```shell
git branch
```
Rename Master branch to main
```shell
git branch -M main

```
Create a new branch at the current commit
```shell
git branch [branch-name]
```
Switch to another branch and check it out into your working directory
```shell
git checkout
```
Merge the specified branch’s history into the current one
```shell
git merge [branch]
```
Show all commits in the current branch’s history
```shell
git log
```
Visualize log tree
```shell
$ git log --oneline --decorate --graph --all
```

## INSPECT AND COMPARE
[Back to summary](#Git)  
Show the commit history for the currently active branch
```shell
git log
```
Show the commits on branchA that are not on branchB
```shell
git log branchB..branchA
```
Show the commits that changed file, even across renames
```shell
git log --follow [file]
```
Show the diff of what is in branchA that is not in branchB
```shell
git diff branchB...branchA
```
Show any object in Git in human-readable format
```shell
git show [SHA]
```

## TRACKING PATH CHANGES
[Back to summary](#Git)  
Delete the file from project and stage the removal for commit
```shell
git rm [file]
```
Change an existing file path and stage the move
```shell
git mv [existing-path] [new-path]
```
Show all commit logs with indication of any paths that moved
```shell
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
```shell
git config --global core.excludesfile [file]
```

## SHARE AND UPDATE
[Back to summary](#Git)  
Add a git URL as an alias
```shell
git remote add [alias] [url]
```
Fetch down all the branches from that Git remote
```shell
git fetch [alias]
```
Merge a remote branch into your current branch to bring it up to date
```shell
git merge [alias]/[branch]
```
Transmit local branch commits to the remote repository branch
```shell
git push [alias] [branch]
```
Fetch and merge any commits from the tracking remote branch
```shell
git pull
```

## REWRITE HISTORY
[Back to summary](#Git)  
Apply any commits of current branch ahead of specified one
```shell
git rebase [branch]
```
Clear staging area, rewrite working tree from specified commit
```shell
git reset --hard [commit]
```

## TEMPORARY COMMITS
[Back to summary](#Git)  
Save modified and staged changes
```shell
git stash
```
List stack-order of stashed file changes
```shell
git stash list
```
Write working from top of stash stack
```shell
git stash pop
```
Discard the changes from top of stash stack
```shell
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
- [pip](#pip)
- [venv](#venv)
- [Django](#Django)
- [Pygame](#Pygame)
- [PySimpleGUI](#PySimpleGUI)

# pip
[Back to summary](#Python)  
The pip module is the default pakage manager for python, very similar to npm for node.  
To install a module
```shell
pip install <package_name>
pip3 install <package_name>
```
To update
```shell
pip install <package_name> --upgrade
pip install <package_name> -U
```
A useful module to check and update every installed module
```shell
pip install pip-review

pip-review --interactive
requests==0.14.0 is available (you have 0.13.2)
Upgrade now? [Y]es, [N]o, [A]ll, [Q]uit y
```
To unsinstall
```shell
pip uninstall <package_name>
```
Install all module from a list of modules file
```shell
pip install -r requirements.txt
```
To create that file according to what is installed (best use with virtual env)
```shell
pip freeze > requirements.txt
```

# venv
[Back to summary](#Python)  
Create a virtual env
```shell
python -m venv venv_name
```
activate venv for that terminal session
on unix
```shell
source venv_name/bin/activate
```
on windows
```shell
source venv_name/Scripts/activate
```
to desactivate venv
```shell
deactivate
```

# Django
[Back to summary](#Python)  
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
```shell
mkdir project_name && cd $_
```
Create venv for the project
```shell
python -m venv env_name   # PC
python3 -m venv env_name  # Mac
```
Activate environnement (Replace "bin" by "Scripts" in Windows)
```shell
source env_name\bin\activate     # Mac
source env_name\Scripts\activate # PC
```
Install Django (and others dependencies if needed)
```shell
pip install django
```
Create requirements file
```shell
pip freeze > requirements.txt
```
Use this commmand to install all required files based on your pip freeze command
```shell
pip install -r requirements.txt
```
Version control initialisation, be sure to create appropriate gitignore
```shell
git init
```


## Create project
[back to summary](#Django)  
This will create a mysite directory in your current directory the manage.py file
```shell
django-admin startproject mysite (or I like to call it config)
```

You can check that everything went fine
```shell
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
```shell
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
```shell
python manage.py makemigrations (app_name)
```
Check the SQL commands that migration would run (identifier is given with makemigrations command).
```shell
python manage.py sqlmigrate #identifier
```
Check for any problems in your project without migrate database
```shell
python manage.py check
```
Create tables and fields in database based on your models
```shell
python manage.py migrate
```
Hop into the interactive Python shell and play around with the free API Django gives you
```shell
python manage.py shell
```

## Administration
[back to summary](#Django)  
Create a user who can login to the admin site
```shell
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
```shell
mkdir app_name/management app_name/management/commands && cd $_
```
Create a python file with your command name
```shell
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
```shell
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
```shell
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
```shell
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
```shell
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
```shell
touch app_name\templatetags\__init__.py
```
Create a python file with the name of the filter
```shell
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
```shell
pip install psycog2 django-heroku gunicorn
```
updtate requirements.txt
```shell
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

# Pygame
[back to summary](#Python)
- [Pygame Project Skeleton](#Pygame-Project-Skeleton)
- [Surfaces](#Surfaces)
- [Rect](#Rect)
- [Collisions](#Collisions)
- [Keyboard](#Keyboard)
- [Mouse](#Mouse)
- [Timer](#Timer)
- [Sprites](#Sprites)
- [Group](#Group)
- [Game state](#Game-state)
- [Animation](#Animation)
- [Level](#Level)


## Pygame Project Skeleton
Here is a good starting point of any pygame project  
[back to summary](#Pygame)  
```python
import pygame
import sys

SCREEN_WIDTH = 1200
SCREEN_HEIGHT = 700
FRAMERATE = 60

# Pygame init
pygame.init()
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Window title")
clock = pygame.time.Clock()

while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
    
    screen.fill("black")
    
    pygame.display.update()
    clock.tick(FRAMERATE) 
    
```

## Surfaces
[back to summary](#Pygame)  
Everything you want to display in pygame, you have to put it on a surface. Althougth, display is also a surface.  
Image in a surface can be plain color, rendered text or an imported image file.  
Every regular surfaces needs to be put on the display surface to be visible.  
Surfaces a defined by a size (a tuple width and height)  
```python

color = "red" # Color can be a color name string, Hex color string or a RGB tupple
position = (50,50) # reference point is top-left

# plain color
width = 10
height = 15
plain_color_surface = pygame.Surface((width, height))
plain_color_surface.fill(color) 

# imported image. Here size is defined by image size
image_surface = pygame.image.load("image path") 
image_surface.convert() # better perf with but no transparency
image_surface.convert_alpha() # same with transparency

# rendered text
string_to_render = "test string"
font_size = 50
string_font = pygame.font.Font("path to a font", font_size)
string_surf = string_font.render(string_to_render, antialias=False, color)

while True:

   # display surface
   screen.blit(plain_color_surface, position)
   screen.blit(string_surf, position)
   screen.blit(image_surface, position)
   
   # Check pygame.transform in documentation to scale, rotate etc...
```

## Rect
[back to summary](#Pygame)  
The 2 core functions of rectangles are precise positionning of surfaces and basic collisions.  
You can get the rectangle of a surface using the get_rect() method  
```python
test_rect = test_surf.get_rect(midtop=(50, 120))
```
Once you have a rect object, it has several virtual attributes which can be used to move and align the Rect.  
```
x,y
top, left, bottom, right
topleft, bottomleft, topright, bottomright
midtop, midleft, midbottom, midright
center, centerx, centery
size, width, height
w,h
```
Examples
```python
rect1.right = 10
rect2.center = (20,30)
```
You can also use rectangles to draw. This allow you to draw plain color rectangle without creating a surface first
```python
pygame.draw.rect(screen_surf, color, rect)
# check documentation for other shapes
```

## Collisions
[back to summary](#Pygame)  
You can check if a rectangle collides with another with colliderect() method  
Returns 0 or 1  
```python
rect1.colliderect(rect2)
```
You can chec if a point is inside a rect using collidepoint() method
Returns 0 or 1
```python
rect.collidepoint((x,y))
```
It is way most convenient to check for sprite collision.  
Using spritecollide() method
```Python
pygame.sprite.spritecollide(sprite, group, bool) # Bool to True kills the group's sprite when there is collision
# returns a list of collided sprites
```

## Keyboard
[back to summary](#Pygame)  
Getting player's keyboard inputs can be achieved by two manner  
pygame.key  
```python
keys = pygame.key.get_pressed()
space_key = keys[pygame.K_SPACE]
```
event loop
```python
for event in pygame.event.get()
    if event.type == pygame.KEYDOWN:
        key = event.key
```
When you I choose which one?  
- Choose pygame.key inside classes  
- For more general stuff, like closing the window, event loop is a better place  

## Mouse
[back to summary](#Pygame)  
Getting the mouse position can be achieved by 2 manner  
pygame.mouse:  
```python
mouse_pos = pygame.mouse.get_pos()
```
event loop:
```python
for event in pygame.event.get()
    if event.type == pygame.MOUSEMOTION:
        mouse_pos = event.pos
```
Same for mouse buttons    
pygame.mouse:  
```python
pygame.mouse.get_pressed()
# returns booleans of (bt1, bt2, bt3)
```
event loop:  
```python
for event in pygame.event.get()
    if event.type == pygame.MOUSEBUTTONDOWN:
        mouse_button = event.button
    if event.type == pygame.MOUSEBUTTONUP:
        mouse_button = event.button
```

## Timer
[back to summary](#Pygame)  
Timers are useful for logic and animation.  
They are created by following 3 steps:  
- create a customm userevent  
- trigger that event at a given interval  
- add code in event loop to be execute when the timer ticks  
You should increment timer reference value each time you create one to ot intefere with in-built userevent  
```python
timer1 = pygame.USEREVENT + 1
timer2 = pygame.USEREVENT + 2

pygame.time.set_timer(timer1, delay)

# In game loop
for event in pygame.event.get()
    if event.type == timer1:
        # Do something
```

## Sprites
[back to summary](#Pygame)  
Sprite class is a class that contains a surface and a rectangle with dedicated methods.  
Just inherit from sprite class to get access to all those features.  
But to draw sprites, there is a different methodology:  
- first create sprite  
- place sprites in Group or GroupSingle  
- draw/update all sprites in that group  
```python
class Player(pygame.sprite.Sprite):
	def __init__(self):
		super().__init__()
		self.image = pygame.image.load("image path").convert_alpha()
		self.rect = self.image.get_rect(midbottom = (200, 300))
		
player = Player()
```

## Group
[back to summary](#Pygame)  
2 types of groups are avaible:  
- Group for multiple sprites  
- GroupSingle for a single sprite  
Notice that to check sprites collisions, sprites have to be in a different group  
```python
player = pygame.sprite.GroupSingle()
player.add(Player())

mobs = pygame.sprite.Group()
mobs.add(Mob())
```
To Access to sprite object inside the group
```python
player.sprite # --> A single sprite
mobs.sprites() # --> A list of sprites
```
Empty a group
```python
mobs.empty()
```
GroupSingle and Group objects have a draw() method  
```python
# In game loop
player.draw(screen)
mobs.draw(screen)
```

## Game state
[back to summary](#Pygame)  
switching to different game states is very easy.  
We can do that by a simple if statement inside the game loop.  
Here is an exemple for a game over
```python
game_active = True

while True:
	# event loop
	#...
	
	if game_active:
		# game logic
	
	else:
		# game over logic or break to exit app
	
```
## Animation
[back to summary](#Pygame)  
Animation in fact is just an image replaced by a slitly different one, fast enough, to get the feeling that it is moving.  
All we have to do is:
- assign an image to a surface
- draw that surface
- update that surface with a new image
- erase the old surface
- draw the new surface
This can be achieve by different manner, but the simplest is to re-draw the backgroung at each recursion of the game loop.
```python
player_frame1 = pygame.image.load("path/to/frame1")
player_frame2 = pygame.image.load("path/to/frame2")
player_frame3 = pygame.image.load("path/to/frame3")

player_frames = [player_frame1, player_frame2, player_frame3]
player_indice = 0

player_surf = player_frames[player_indice]
player_rect = player_surf.get_rect()


while True
	...
	...
	screen.blit(background_surf, background_rect)
	
	# Animate player
	player_indice += 0.1
	if player_indice >= len(player_frames)
		player_indice = 0
	player_surf = player_frames[int(player_indice)]
	
	screen.blit(player_surf, player_rect)
	
	...
```
## Level
[back to summary](#Pygame) 
The concept of making a level is based on looping through strings that we loop through a list and display something based on which character we get.  
To keep it simple, let say we only want to display something when we get an "X".  
Example of level
```python
level = [
'                       ',
'                XX     ',
'             XX        ',
'       XXXX            ',
'     XXXXXXX           ',
'XXXXXXXXXXXXXXXXXXXXXXX',
]
```
As you can see, we have here a floor and some plateforms.  
Now what we want is create a group of sprites represanting every "X" of the level.  
We can say that each "X" is like a tile. Let's create that class
```python
class Tile(pygame.sprite.Sprite):
	def __init__(self, pos, size):
		super().init()
		self.image = "Whatever surface you want"
		self.rect = self.image.get_rect(topleft=pos)
```
As you can see, we have to specify a size, otherwize, our level will be pixel by pixel and we'll not be able to see something.  
The pos argument is the coordinate we will get by looping through the level.  
All we will have to do then, is to draw every sprites.  
Let's create the level class
```python
tile_size = 64

class Level:
	def __init__(self, level, surface):
		self.display_surface = surface # will be screen actualy
		self.setup_level(level)
		
	def setup_level(self, level)
		self.tiles = pygame.sprite.Group()
		for row_index, row in enumerate(level):
			for col_index, cell in enumerate(row):
				if cell == "X":
					x = col_index * tile_size
					y = row_index * tile_size
					tile = Tile((x,y ), tile_size)
					self.tiles.add(tile)
	
	def run(self):
		self.tiles.draw(self.display_surface)
```
Just create level instance outside game loop and call the level.run() method inside the loop. Boom! You have a level.  
Last tips: 
- for screen height, you can use len(level) * tile_size if you don't plan to scroll verticaly
- for screen width, len(level[0]) * tile_size

## Camera
[back to summary](#Pygame) 


--- Work In Progress --

# PySimpleGUI
[back to summary](#Python)
- [Indroduction](#Indroduction)
- [keys](#keys)
- [Themes](#Themes)

## Indroduction
[back to summary](#PySimpleGUI) 
PySimpleGUI is a easy library to make simple GUI apps.  
The core concept of this library is that the GUI is separate in rows, each row is a list, all those is put in a layout.  
Let's get started with the basic exemple of a GUI app whith this library.
```python
import PySimpleGUI as sg

title = "Converter" # window title

layout = [
    [sg.Text("A text box"), sg.Spin(["a spin box", "That let's you", "choose an item"])], # You can see here we have 2 boxes in that row
    [sg.Text("Enter a value"), sg.Input(key="-INPUT-"), sg.Button("Convert", key="-BUTTON-")],
    [sg.Text("", key="-RESULT-")]
]

window = sg.Window(title, layout) # create the window object

while True:
    event, values = window.read()
    if event == sg.WIN_CLOSED:
        break
    if event == "-BUTTON-":
        entry = values["-INPUT-"] # here is how you get the value of the input box

window.close()
```
## keys
[back to summary](#PySimpleGUI) 
In the exemple above, you can see the uses of keys. Putting the key name between 2 "-" is convention.  
Keys are useful to identify which box we refers to. For example, if you have two buttons with "OK" text inside your app, you'll have to assign a key to at least one of these button if you want them to act separatly (what you always want to do in fact) 

## Themes
[back to summary](#PySimpleGUI) 
Themes are a fast way to change default aspect of pySimpleGUI apps.  
Apply a theme is as simple as call the sg.theme() method before creating the window
```python
sg.theme("DarkTeal16")
```
calling 
```python
sg.theme_previewer() 
```
will help you choose your theme


--- Work In Progress --



# Javascript
[Back to summary](#My-Programming-Cheatsheets)  
- [Working With Array](#Working-With-Array)
- [Working With Strings](#Working-With-Strings)
- [Working With Objects](#Working-With-Objects)
- [Loops](#Loops)
- [Node JS](#nodeJS)
- [Tests](#Tests)
- [ExpressJS](#expressJS)
- [EJS](#EJS)

## Working With Array
[Back to summary](#Javascript) 
### reduce()  
The reduce() method executes a user-supplied "reducer" callback function on each element of the array, in order, passing in the return value from the calculation on the preceding element. The final result of running the reducer across all elements of the array is a single value.

```javascript
function find_average(array) {
//   acc is accumulator and curr is current value being processed
//   0 is the initial value of the accumulator
  return array.reduce((acc, curr) => {
      return acc + curr
    }, 0) / array.length;
}
```
### reverse()
The reverse() METHOD reverses an array in place. The first array element becomes the last, and the last array element becomes the first.
```javascript
const array1 = ['one', 'two', 'three'];
console.log('array1:', array1);
// expected output: "array1:" Array ["one", "two", "three"]

// Careful: reverse is destructive -- it changes the original array.
console.log('array1:', array1);
// expected output: "array1:" Array ["three", "two", "one"]
```
### join()
The join() METHOD creates and returns a new string by concatenating all of the elements in an array (or an array-like object), separated by commas or a specified separator string. If the array has only one item, then that item will be returned without using the separator.
```javascript
console.log(elements.join());
// expected output: "Fire,Air,Water"

console.log(elements.join(''));
// expected output: "FireAirWater"

console.log(elements.join('-'));
// expected output: "Fire-Air-Water"
```
### map()
The map() METHOD creates a new array populated with the results of calling a provided function on every element in the calling array.
```javascript
// Exemples
// Return a new array with the square root of all element values:
const numbers = [4, 9, 16, 25];
const newArr = numbers.map(Math.sqrt)
// [2, 3, 4, 5]

// Multiply all the values in an array with 10:
const numbers = [65, 44, 12, 4];
const newArr = numbers.map(myFunction)

function myFunction(num) {
  return num * 10;
}

// Convert array of strings to an array of numbers
["1", "2", "3"].map((str) => parseInt(str)));
```
### entries()
The entries() method returns an object of type Array Iterator which contains the couple Key/value for each elements of the array
```javascript
const array1 = ['a', 'b', 'c'];

const iterator1 = array1.entries();

console.log(iterator1.next().value);
// expected output: Array [0, "a"]

console.log(iterator1.next().value);
// expected output: Array [1, "b"]
```

### Utility Functions
#### some
Parameters:  
- predicate - Function that returns true or false.  
- array - List of items to test.  
Description:  
- If predicate returns true for any item, some returns true. Otherwise it returns false.  
```javascript
const some = (predicate, array) => {
  array.reduce((acc, value) => {
    acc || predicate(value);
  }, false);
};
```
#### all
Parameters:  
- predicate - Function that returns true or false.  
- array - List of items to test.  
Description:
- If predicate returns true for every item, all returns true. Otherwise it returns false.
```javascript
const all = (predicate, array) => {
  array.reduce((acc, value) => {
    acc && predicate(value);
  }, true);
};
```
#### none
Parameters:  
- predicate - Function that returns true or false.
- array - List of items to test.
Description:  
- If predicate returns false for every item, none returns true. Otherwise it returns false.
```javascript
const none = (predicate, array) => {
  array.reduce((acc, value) => {
    !acc && !predicate(value);
  }, false);
};
```
#### filter
Parameters:  
- predicate - Function that returns true or false.
- array - List of items to filter.
Description:  
- Returns a new array. If predicate returns true, that item is added to the new array. Otherwise that item is excluded from the new array.
```javascript
const filter = (predicate, array) =>
  array.reduce((newArray, item) => {
    if (predicate(item) === true) {
      newArray.push(item);
    }

    return newArray;
  }, []);
```
#### reject
Parameters:  
- predicate - Function that returns true or false.
- array - List of items to filter.
Description:  
- Just like filter, but with the opposite behavior.
-If predicate returns false, that item is added to the new array. Otherwise that item is excluded from the new array.
```javascript
const reject = (predicate, array) =>
  array.reduce((newArray, item) => {
    if (predicate(item) === false) {
      newArray.push(item);
    }

    return newArray;
  }, []);
```
#### find
Parameters:  
- predicate - Function that returns true or false.
- array - List of items to search.
Description:  
- Returns the first element that matches the given predicate. If no element matches then undefined is returned.
```javascript
const find = (predicate, array) =>
  array.reduce((result, item) => {
    if (result !== undefined) {
      return result;
    }

    if (predicate(item) === true) {
      return item;
    }

    return undefined;
  }, undefined);
```

#### partition
Parameters:
-predicate - Function that returns true or false.
-array - List of items.
Description:
- "Partitions" or splits an array into two based on the predicate. If predicate returns true, the item goes into list 1. Otherwise the item goes into list 2.
```javascript
const partition = (predicate, array) =>
  array.reduce(
    (result, item) => {
      const [list1, list2] = result;

      if (predicate(item) === true) {
        list1.push(item);
      } else {
        list2.push(item);
      }

      return result;
    },
    [[], []]
  );
```
#### pluck
Parameters
- key - Key name to pluck from the object
- array - List of items.
Description
- Plucks the given key off of each item in the array. Returns a new array of these values.
```javascript
const pluck = (key, array) =>
  array.reduce((values, current) => {
    values.push(current[key]);

    return values;
  }, []);

// Examples
pluck('name', [{ name: 'Batman' }, { name: 'Robin' }, { name: 'Joker' }]);
// ['Batman', 'Robin', 'Joker']

pluck(0, [[1, 2, 3], [4, 5, 6], [7, 8, 9]]);
// [1, 4, 7]
```
#### scan
Parameters
- reducer - Standard reducer function that receives two parameters - the accumulator and current element from the array.
- initialValue - The initial value for the accumulator.
- array - List of items.
Description
- Works just like reduce but instead just the single result, it returns a list of every reduced value on the way to the single result.
```javascript
const scan = (reducer, initialValue, array) => {
  const reducedValues = [];

  array.reduce((acc, current) => {
    const newAcc = reducer(acc, current);

    reducedValues.push(newAcc);

    return newAcc;
  }, initialValue);

  return reducedValues;
};

// Examples
const add = (x, y) => x + y;
const multiply = (x, y) => x * y;

scan(add, 0, [1, 2, 3, 4, 5, 6]);
// [1, 3, 6, 10, 15, 21] - Every number added from 1-6

scan(multiply, 1, [1, 2, 3, 4, 5, 6]);
// [1, 2, 6, 24, 120, 720] - Every number multiplied from 1-6
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

// Also works with arrays
const array1 = ['one', 'two', 'three'];

Object.entries(array1)
// [["0", "one"], ["1", "two"], ["2", "three"]]
```
## Loops
[Back to summary](#Javascript) 
  
JavaScript supports different kinds of loops:
- for - loops through a block of code a number of times
- for/in - loops through the properties of an object
- for/of - loops through the values of an iterable object
- while - loops through a block of code while a specified condition is true
- do/while - also loops through a block of code while a specified condition is true

### for
Basic for loop
```javascript
for (let i = 0; i < 5; i++) {
  // Executed 5 times
  // At each excecution, i is incremented by 1
  ...
}
```
### for ... in
Loops through enumerable properties of a given object
```javascript
let myArray = ["a", "b", "c"]
let myObject = {
  a: "one",
  b: "two",
  c: "three"
}

for(index in myArray){
  console.log(index)
  // 0
  // 1
  // 2
}

for(key in myObject){
  console.log(key)
  // a
  // b
  // c
}
```
### for ... of
Loops through values of an array
```javascript
let myArray = ["a", "b", "c"]

for(let value of myArray){
  console.log(value)
  // "a"
  // "b"
  // "c"
}
```
### while
Basic while loop, loops whenever the condition is true
```javascript
let n = 0;
let x = 0;
while (n < 3) {
  n++;
  x += n;
}
```
### do ... while
Same as while loop but because the condition is tested after the instruction, it will be executed at least one time.
```javascript
let i = 0;
do {
  i += 1;
  console.log(i);
} while (i < 5);
```

## nodeJS
[Back to summary](#Javascript)  
Init node to create package.json
```shell
npm init 
npm init -y (validate every default fields)
```
Install external node module for your project
```shell
npm install package_name
```
Install external node module to your system
```shell
npm install -g package_name
```

## Tests
[Back to summary](#Javascript)  
We can test node apps using Assert and Mocha  
First require assert in your test file, for exemple, index.test.js
```javascript
const assert = require('assert').strict;
// strict property alows us to use specials equalities tests recommended by node  
```
Next change "test" value like this in package.json
```json
...
"scripts": {
    "test": "mocha index.test.js"
},
...
```
We can mow write a test in our test file
```javascript
describe("Test group name", function() { 		 // We "describe" a test group
    it("should give a given result", function() {	 // Be descriptive in your tests name
    	// some code
    });
    
    it("should do a specific thing", function() {	 // Be descriptive in your tests name
        // some code
    });
});

describe("An other test group name", function() { 		 // We "describe" an other test group
    it("should give a given result", function() {	 // Be descriptive in your tests name
        // some code
    });
    
    it("should do a specific thing", function() {	 // Be descriptive in your tests name
        // some code
    });
});
```
In your test code you can use for exemple
```javascript
// Check equality
assert.strictEqual(content, expectedFileContents)

// Check inequality
assert.notStrictEqual(content, expectedFileContents)

// Throw error
assert.throws(fn, error, message)
/*
fn <Function> 
error <RegExp> | <Function> | <Object> | <Error>
message <string>

Expects the function fn to throw an error.
error and message are optional
*/

```
To run the test
```shell
npm test
```
Output if test pass
```shell
> todos@1.0.0 test your_file_path/your_app
> mocha index.test.js



Test group name
    ✓ should give a given result
    ✓ should do a specific thing
    
An other test group name
    ✓ should give a given result
    ✓ should do a specific thing

  3 passing (36ms)
```
For async code, better use async / await with mocha, less code and more readable
```javascript
...
describe("saveToFile()", function() {
    it("should save a single TODO", async function() {
        let todos = new Todos();
        todos.add("save a CSV");
        await todos.saveToFile();

        assert.strictEqual(fs.existsSync('todos.csv'), true);
        let expectedFileContents = "Title,Completed\nsave a CSV,false\n";
        let content = fs.readFileSync("todos.csv").toString();
        assert.strictEqual(content, expectedFileContents);
    });
});
```
Hooks also exists  
- before	This hook is executed BEFORE the FIRST test
- beforeEach	This hook is executed BEFORE EACH case tests
- after		This hook is executed AFTER the last case test
- afterEach	This hook isexecuted AFTER EACH tests
```javascript
describe("saveToFile()", function () {
    beforeEach(function () {
    	// We create a todo and add a value to it before each case tests
        this.todos = new Todos();
        this.todos.add("save a CSV");
    });

    afterEach(function () {
    	// After each case tests, if a todos.csv file exists, we delete it
        if (fs.existsSync("todos.csv")) {
            fs.unlinkSync("todos.csv");
        }
    });
```
Awesome, our tests are automated and organized, easy to run, easy to maintain

## expressJS
[Back to summary](#Javascript) 
Install express
```shell
npm install express
```
Install BODY-PARSER for forms management
```shell
npm i body-parser
```
Install EJS for templating
```shell
npm install ejs
```
Install NODEMON to autorefresh server at any modification
```shell
npm install -g nodemon
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
  someInfoVar = "Some info"
  context = {
    someInfo: someInfoVar // In template, access this value with someInfo key
  }
  res.render(__dirname + "/views/home.ejs", context);
});


// #### Port Listening ####
const PORT = process.env.PORT || 3000
app.listen(PORT, function () {
  console.log(`Server started on port ${PORT}`);
});

```
Work with API in node using axios
```javascript
// Install axios package first
var axios = require("axios").default;

var options = {
  method: 'GET',
  url: 'https://url-of-the-api.com',
  params: {param1: 'value', param2: 'value'},
  headers: {
    // Read API's doc to found appropriate headers
    'host': 'host-url.com',
    'key': 'SIGN-UP-FOR-KEY'
  }
};

axios.request(options).then((response) => {
	console.log(response.data);
}).catch((error) => {
	console.error(error);
});
```
Serve Static files 
```javascript
app.use(express.static('public'));

/* You can mow access files that are in public folder
Examples:
  http://localhost:3000/css/style.css
  http://localhost:3000/js/app.js
  http://localhost:3000/images/bg.png
*/
```
Deploy App to heroku
```
Follow well made tutorial from heroku's devcenter documentation
https://devcenter.heroku.com/articles/deploying-nodejs
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

# MongoDB
[Back to summary](#My-Programming-Cheatsheets)  

- [Mongo Shell](#Mongo-Shell)
### CRUD operations
- [Create](#Create)
- [Read](#Read)
- [Update](#Update)
- [Delete](#Delete)
### ODM
- [Mongoose](#Mongoose)

## Mongo Shell
[Back to summary](#MongoDB)  
open mongo shell
```shell
mongo
```
Commands list
```shell
help
```
Show Databases, collections, users...
```shell
show dbs
show collections
show users
```
Switch to a specific database (create it if doesn't exist)
```shell
use db_name
```
To show in which DB you currently are
```shell
db
```

## Create
[Back to summary](#MongoDB)  

 - db.collection.insertOne() inserts a single document into a collection. If the document does not specify an _id field, MongoDB adds the _id field with an ObjectId value to the new document.  
```javascript
db.movies.insertOne( // If the movies collection (SQL table equivalent)
  {		     // doesn't exist, it will be created
    title: "The Favourite",
    genres: [ "Drama", "History" ],
    runtime: 121,
    rated: "R",
    year: 2018,
    directors: [ "Yorgos Lanthimos" ],
    cast: [ "Olivia Colman", "Emma Stone", "Rachel Weisz" ],
    type: "movie"
  }
)
```

- db.collection.insertMany() can insert multiple documents into a collection. Pass an array of documents to the method. If the documents do not specify an _id field, MongoDB adds the _id field with an ObjectId value to each document
```javascript
db.movies.insertMany([
   {
      title: "Jurassic World: Fallen Kingdom",
      genres: [ "Action", "Sci-Fi" ],
      runtime: 130,
      rated: "PG-13",
      year: 2018,
      directors: [ "J. A. Bayona" ],
      cast: [ "Chris Pratt", "Bryce Dallas Howard", "Rafe Spall" ],
      type: "movie"
    },
    {
      title: "Tag",
      genres: [ "Comedy", "Action" ],
      runtime: 105,
      rated: "R",
      year: 2018,
      directors: [ "Jeff Tomsic" ],
      cast: [ "Annabelle Wallis", "Jeremy Renner", "Jon Hamm" ],
      type: "movie"
    }
])
```

## Read
[Back to summary](#MongoDB)  

- Use the db.collection.find() method in the MongoDB Shell to query documents in a collection. To read all documents in the collection, pass an empty document as the query filter parameter to the find method.
```javascript
db.movies.find() // all
db.accounts.findOne( { account_id: 893421 } ) // One 
```

- To select documents which match an equality condition, specify the condition as a "field: value" pair in the query filter document.
```javascript
db.movies.find({
  "title": "Titanic" 
  })
```

- Use [query operators](https://docs.mongodb.com/manual/reference/operator/query/#query-selectors) in a query filter document to perform more complex comparisons and evaluations. Query operators in a query filter document have the following form: { field1: { operator1: value1 }, ... }
```javascript
db.movies.find({
  rated: {
    $in: ["PG", "PG-13"]
    }
  })	
```

- A compound query can specify conditions for more than one field in the collection's documents. Implicitly, a logical AND conjunction connects the clauses of a compound query so that the query selects the documents in the collection that match all the conditions.
```javascript
db.movies.find({
  countries: "Mexico",
  imdb.rating: {
    $gte: 7
    }
  })	
```
	
## Update
[Back to summary](#MongoDB)  

To update a document, MongoDB provides [update operators](https://docs.mongodb.com/manual/reference/operator/update/), such as $set, to modify field values.
- Use the db.collection.updateOne() method to update the first document that matches a specified filter.
```javascript
db.movies.updateOne( { title: "Tag" },
{
  $set: {
    plot: "One month every year, five highly competitive friends
           hit the ground running for a no-holds-barred game of tag"
  }
  { $currentDate: { lastUpdated: true } }
})
```

- Use the db.collection.updateMany() to update all documents that match a specified filter.
```javascript
db.listingsAndReviews.updateMany(
  { security_deposit: { $lt: 100 } },
  {
    $set: { security_deposit: 100, minimum_nights: 1 }
  }
)
```

-To replace the entire content of a document except for the _id field, pass an entirely new document as the second argument to db.collection.replaceOne(). When replacing a document, the replacement document must contain only field/value pairs. Do not include update operators expressions. The replacement document can have different fields from the original document. In the replacement document, you can omit the _id field since the _id field is immutable; however, if you do include the _id field, it must have the same value as the current value.
```javascript
db.accounts.replaceOne(
  { account_id: 371138 },
  { account_id: 893421, limit: 5000, products: [ "Investment", "Brokerage" ] }
)
```

## Delete
[Back to summary](#MongoDB)  

- To delete all documents from a collection, pass an empty filter document {} to the db.collection.deleteMany() method.
```javascript
db.movies.deleteMany({})
```

- You can specify criteria, or filters, that identify the documents to delete. The filters use the same syntax as read operations.
```javascript
db.movies.deleteMany( { title: "Titanic" } )
```

- To delete at most a single document that matches a specified filter (even though multiple documents may match the specified filter) use the db.collection.deleteOne() method.
```javascript
db.movies.deleteOne( { cast: "Brad Pitt" } )
```

## Mongoose
[Back to summary](#MongoDB)  

- [Terminologies](#Terminologies)
- [Schemas](#Schemas)
- [Models](#Models)
- [Data Validation](#Data-Validation)
- [Fetch Record](#Fetch-Record)
- [Update Record](#Update-Record)
- [Delete Record](#Delete-Record)
- [Helpers](#Helpers)


### Terminologies
[Back to summary](#Mongoose)  

#### Collections
‘Collections’ in Mongo are equivalent to tables in relational databases. They can hold multiple JSON documents.

#### Documents
‘Documents’ are equivalent to records or rows of data in SQL. While a SQL row can reference data in other tables, Mongo documents usually combine that in a document.

#### Fields
‘Fields’ or attributes are similar to columns in a SQL table.

#### Schema
While Mongo is schema-less, SQL defines a schema via the table definition. A Mongoose ‘schema’ is a document data structure (or shape of the document) that is enforced via the application layer.

#### Models
‘Models’ are higher-order constructors that take a schema and create an instance of a document equivalent to records in a relational database.

### Schemas
[Back to summary](#Mongoose)  

Everything in Mongoose starts with a Schema. Each schema maps to a MongoDB collection and defines the shape of the documents within that collection.  
Each key in our code blogSchema defines a property in our documents which will be cast to its associated [SchemaType](#https://mongoosejs.com/docs/schematypes.html).
```javascript
import mongoose from 'mongoose';
  const { Schema } = mongoose;
  
  mongoose.connect("mongodb://localhost:27017/booksDB"); // Connect to booksDB and use it. 
  							 // Create it if inexistant 

  const blogSchema = new Schema({
    title:  String, // String is shorthand for {type: String}
    author: String,
    body:   String,
    comments: [{ body: String, date: Date }],
    date: { type: Date, default: Date.now },
    hidden: Boolean,
    meta: {
      votes: Number,
      favs:  Number
    }
  });
  
  // It's good practice to close connection to db when uneeded
  mongoose.connection.close().then(() => {
    console.log("\nDisconnect...");
  });
```

To use our schema definition, we need to convert our blogSchema into a Model we can work with. To do so, we pass it into mongoose.model(modelName, schema)
```javascript
const Blog = mongoose.model('Blog', blogSchema);
// ready to go!
```

By default, Mongoose adds an _id property to your schemas.
```javascript
const schema = new Schema();

schema.path('_id'); // ObjectId { ... }
```

### Models
[Back to summary](#Mongoose)  

Mongoose Schema vs. Model:
- A Mongoose model is a wrapper on the Mongoose schema. A Mongoose schema defines the structure of the document, default values, validators, etc., whereas a Mongoose model provides an interface to the database for creating, querying, updating, deleting records, etc.

```javascript
// Defining Model
MyModel = mongoose.model('ModelsName', modelSchema)

// Create Instance
let myInstance = new MyModel({
	field: "value"
)}

myInstance.save()
   .then(doc => {
     console.log(doc)
   })
   .catch(err => {
     console.error(err)
   })

/*
{ 
  _id: 5a78fe3e2f44ba8f85a2409a, -> The _id field is auto-generated by Mongo and is a primary key of the collection. 
  				    Its value is a unique identifier for the document.
  field: "value", -> The value of the field is returned
  __v: 0 -> __v is the versionKey property set on each document when first created by Mongoose. 
  	    Its value contains the internal revision of the document.
}
*/
```

### Data Validation
[Back to summary](#Mongoose)  

When creating your schemas, you can specify [validation rules](https://mongoosejs.com/docs/validation.html).  
Each field type can have the required validator.  
If validation doesn't pass, it will raise a ValidationError and give you details of that failure.
```javascript
const mongoose = require("mongoose");

const exempleSchema = new mongoose.Schema ({
  firstField: String,
  FieldWithValidation: {
    // Mongoose will check if the value is a number between 1 and 10
    type: Number,
    min: 1,
    max: 10,
    // We define here that FieldWithValidation field is required
    // If we don't provide this field, it will raise an error when we attempt to save the document
    required: true
  }
});
```


### Fetch Record
[Back to summary](#Mongoose)  

Use find() method to fetch record
```javascript
MyModel
  .find({
    field: 'value'   // search query
  })
  .then(doc => {
    console.log(doc)
  })
  .catch(err => {
    console.error(err)
  })
```

### Update Record
[Back to summary](#Mongoose)  

Use findOneAndUpdate() method to update a single record.  
For performance reasons, Mongoose won’t return the updated document so we need to pass an additional parameter to ask for it
```javascript
MyModel
  .findOneAndUpdate(
    {
      field: 'value'  // search query
    }, 
    {
      field: 'new value'   // field:values to update
    },
    {
      new: true,                       // return updated doc
      runValidators: true              // validate before update
    })
  .then(doc => {
    console.log(doc)
  })
  .catch(err => {
    console.error(err)
  })
```

### Delete Record
[Back to summary](#Mongoose)  

Use the findOneAndRemove call to delete a record. It returns the original document that was removed
```javascript
MyModel
  .findOneAndRemove({
    field: 'value'
  })
  .then(response => {
    console.log(response)
  })
  .catch(err => {
    console.error(err)
  })
```

### Helpers
[Back to summary](#Mongoose)  

- Virtual Property  
A virtual property is not persisted to the database. We can add it to our schema as a helper to get and set values.
```javascript
let mongoose = require('mongoose')

let userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String
})

module.exports = mongoose.model('User', userSchema)

/*
Let’s create a virtual property called fullName which can be used to set values on 
firstName and lastName and retrieve them as a combined value when read:
*/
userSchema.virtual('fullName').get(function() {
  return this.firstName + ' ' + this.lastName // Now we can get full name from firstname and lastname
})

userSchema.virtual('fullName').set(function(name) {
  let str = name.split(' ')
  
  // Now we can set fistName and lastName from fullname:
  // model.fullName = 'Thomas Anderson'
  this.firstName = str[0]
  this.lastName = str[1]
})
```
- Instance Methods  
We can create custom helper methods on the schema and access them via the model instance
```javascript
userSchema.methods.getInitials = function() {
  // Returns the initials for the current user
  return this.firstName[0] + this.lastName[0]
}

// This method will be accessible via a model instance
let model = new UserModel({
  firstName: 'Thomas',
  lastName: 'Anderson'
})

let initials = model.getInitials()

console.log(initials) // This will output: TA
```

- Static Methods  
Similar to instance methods, we can create static methods on the schema. Let’s create a method to retrieve all users in the database
```javascript
userSchema.statics.getUsers = function() {
  return new Promise((resolve, reject) => {
    this.find((err, docs) => {
      if(err) {
        console.error(err)
        return reject(err)
      }
      
      resolve(docs)
    })
  })
}

// Calling getUsers on the Model class will return all the users in the database
UserModel.getUsers()
  .then(docs => {
    console.log(docs)
  })
  .catch(err => {
    console.error(err)
  })
```

- Middleware  
Middleware are functions that run at specific stages of a pipeline. Mongoose supports middleware for the following operations
	- Aggregate
	- Document
	- Model
	- Query
For instance, models have pre and post functions that take two parameters
	- Type of event (‘init’, ‘validate’, ‘save’, ‘remove’)
	- A callback that is executed with "this" referencing the model instance
Let’s add two fields called createdAt and updatedAt to our userSchema
```javascript
let mongoose = require('mongoose')

let userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String,
  createdAt: Date,
  updatedAt: Date
})

module.exports = mongoose.model('User', userSchema)
```
When model.save() is called, there is a pre(‘save’, …) and post(‘save’, …) event that is triggered.  
For the second parameter, you can pass a function that is called when the event is triggered.  
These functions take a parameter to the next function in the middleware chain.
Let’s add a pre-save hook and set values for createdAt and updatedAt
```javascript
userSchema.pre('save', function (next) {
  let now = Date.now()
   
  this.updatedAt = now
  // Set a value for createdAt only if it is null
  if (!this.createdAt) {
    this.createdAt = now
  }
  
  // Call the next function in the pre-save chain
  next()    
})
```
Let’s create and save our model
```javascript
let UserModel = require('./user')

let model = new UserModel({
  fullName: 'Thomas Anderson'
}

msg.save()
   .then(doc => {
     console.log(doc)
   })
   .catch(err => {
     console.error(err)
   })
/*
{ _id: 5a7bbbeebc3b49cb919da675,
  firstName: 'Thomas',
  lastName: 'Anderson',
  updatedAt: 2018-02-08T02:54:38.888Z,
  createdAt: 2018-02-08T02:54:38.888Z,
  __v: 0 }
*/
```
- Plugins  
Suppose that we want to track when a record was created and last updated on every collection in our database.  
Instead of repeating the above process, we can create a plugin and apply it to every schema.  
Let’s create a plugin
```javascript
module.exports = function timestamp(schema) {

  // Add the two fields to the schema
  schema.add({ 
    createdAt: Date,
    updatedAt: Date
  })
```
To use this plugin, we simply pass it to the schemas that should be given this functionality
```javascript
let timestampPlugin = require('./plugins/timestamp')

emailSchema.plugin(timestampPlugin)
userSchema.plugin(timestampPlugin)
```

- Query Building  
There are lots of [Queries](https://mongoosejs.com/docs/api/query.html) we can use in mongoose.  
Here is an example
```javascript
UserModel.find()                   // find all users
         .skip(100)                // skip the first 100 items
         .limit(10)                // limit to 10 items
         .sort({firstName: 1}      // sort ascending by firstName
         .select({firstName: true} // select firstName only
         .exec()                   // execute the query
         .then(docs => {
            console.log(docs)
          })
         .catch(err => {
            console.error(err)
          })
```



--- Work In Progress ---
