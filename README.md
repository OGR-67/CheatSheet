# My Programming Cheatsheets

- [Python](https://github.com/OGR-67/CheatSheet/edit/main/README.md#Python)
- [Javascript](#Javascript)

## Python
### Django
- [Preparing Environnement](https://github.com/OGR-67/CheatSheet/edit/main/README.md#Preparing%20Environnement)
- 
#### Preparing Environnement

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

## Javascript
