# My Programming Cheatsheets

- [Python](#Python)
- [Javascript](#Javascript)

# Python
# Django
- [Preparing Environnement](#Preparing%20Environnement)
- [Create project](#Create%20project)
- [Database Setup](#Database-Setup)

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

## Database-Setup
Open up mysite/settings.py. It’s a normal Python module with module-level variables representing Django settings.
If you wish to use another database, install the approp­riate database bindings and change the following keys in the DATABASES 'default' item to match your database connection settings
```python
ENGINE – 'django.db.backends.sqlite3', 'django.db.backends.postgresql', 'django.db.backends.mysql', or 'django.db.backends.oracle'
```

The default value, BASE_DIR / 'db.sqlite3', will store the file in your project directory
NAME – The name of your database. If you’re using SQLite, the database will be a file on your computer; in that case, NAME should be the full absolute path, including filename, of that file.
The default value, BASE_DIR / 'db.sqlite3', will store the file in your project directory.
If you are not using SQLite as your database, additional settings such as USER, PASSWORD, and HOST must be added.
For more details, see the reference documentation for [DATABASES](https://docs.djangoproject.com/en/4.0/ref/settings/#std:setting-DATABASES).

## Javascript
