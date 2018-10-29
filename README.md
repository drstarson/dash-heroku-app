# Dash on Heroku

This is a setup and a template for publishing Dash apps on Heroku. 
The app1.py itself is just an example. 
The detailed instructions are provided below. 

Based on https://www.udemy.com/interactive-python-dashboards-with-plotly-and-dash/

## Deploying App to Heroku

By default Dash apps run on localhost and are launced with app.run_server().

However, there is an easy way to deploy Dash apps into cloud environments. 
Dash uses Flask as its web framework and can be deployed anywhere where Flask can be deployed. Options include Digital Ocean, PythonAnywhere, GCP, AWS, Azure, etc.

Here we are deploying on Heroku.

For more information on deploying Flask apps visit [Flask Deployment](http://flask.pocoo.org/docs/0.12/deploying/) 

For more on Heroku visit [Heroku Intro](https://devcenter.heroku.com/articles/getting-started-with-python#introduction) 

### STEP 1 - Install Heroku and Git

1. Open a Heroku account. Free accounts are available at https://signup.heroku.com/dc 
Follow the instructions to obtain a username and password. Write them down!
2. Log into your Heroku account. It should take you to https://dashboard.heroku.com/apps
3. Click on Python. On the next screen select Set Up. An option should appear to download the Heroku Command Line Interface (CLI). Choose your operating system from the dropdown list and follow the instructions to install the utility. You should have the option to install Git as well.
4. If git was not installed with Heroku CLI, you can download it directly from https://git-scm.com/downloads and follow the instructions for your operating system.

### STEP 2 - Install virtualenv

Install `virtualenv` via `pip install virtualenv`. Virtualenv allows you to create virtual environments for your app that house Python and all the dependencies your app requires. This includes specific version of plotly, dash, and other libraries that you know will work. As new updates become available, they won’t break your app until you’ve had a chance to test them first!

### STEP 3 - Create a Development Folder and cd into it
Create a new folder for your project. This will house the “development” copy of your app:
```
mkdir my_dash_app
cd my_dash_app
```

### STEP 4 - Initialize Git
Initialize an empty git repository `git init`


### STEP 5 (macOS/Linux) - Create, Activate and Populate a virtualenv
Create a virtual environment. We’re calling ours “venv” but you can use any name you want:
`python3 -m virtualenv venv`

Activate the virtual environment:
`source venv/bin/activate`

Install dash and any desired dependencies into your virtual environment
```
$ pip install dash
$ pip install dash-auth
$ pip install dash-renderer
$ pip install dash-core-components
$ pip install dash-html-components
$ pip install plotly (requirement may be satisfied, see above)
```

Install a new dependency gunicorn for deploying the app: `pip install gunicorn`

STEP 6 - Add Files to the Development Folder
The following files need to be added:
* `app1.py`	a Dash application
* `.gitignore`	used by git, identifies files that won’t be pushed to production
* `Procfile`	used for deployment
* `requirements.txt`	describes your Python dependencies, can be created automatically

For freezing requirements: 
`pip freeze > requirements.txt`


### STEP 6 - Log onto your Heroku Account
At the terminal, login using the credentials you established in STEP1: `heroku login`

### STEP 7 - Initialize Heroku, add files to Git, and Deploy

(venv) C:\my_dash_app>heroku create my-dash-app 

You have to change my-dash-app to a unique name. The name must start with a letter and can only contain lowercase letters, numbers, and dashes.

`(venv) C:\my_dash_app>git add .`
Note the period at the end. This adds all files to git (except those listed in .gitignore)

`(venv) C:\my_dash_app>git commit -m "Initial launch"`
Every git commit should include a brief descriptive comment. Depending on your operating system, this comment may require double-quotes (not single-quotes).

`(venv) C:\my_dash_app>git push heroku master `
This deploys your current code to Heroku. The first time you push may take awhile as it has to set up Python and all your dependencies on the remote server.

`(venv) C:\my_dash_app>heroku ps:scale web=1 `
Scaling dynos... done, now running web at 1:Free
This runs the app with a 1 heroku "dyno"

### STEP 8 - Visit Your App on the Web!
You should be able to view your app at https://my-dash-app.herokuapp.com
(changing my-dash-app to the name of your app)

### STEP 9 - Update Your App
Any time you make changes to your app, add new apps to your repo, or install new libraries and/or upgrade existing dependencies in your virtual environment, you want to push the latest updates to Heroku. These are the basic steps:
If installing a new package:
```
$ pip install newdependency
$ pip freeze > requirements.txt
```

If updating an existing package:
```
$ pip install dependency --upgrade
$ pip freeze > requirements.txt
```

In all cases:
```
$ git status # view the changes (optional)
$ git add .  # add all the changes
$ git commit -m "a description of the changes"
$ git push heroku master
```

TROUBLESHOOTING
If your app won’t launch on Heroku, follow this checklist:

* app1.py includes server = app:server
If not, add this line, save the file, then run Git add/commit/push 

* gunicorn installed, and included in requirements.txt
If not, run pip install gunicorn, then pip freeze > requirements.txt, then run Git add/commit/push

*	If unable to trace locally, visit your Heroku dashboard and click on More / View logs


Resources: https://dash.plot.ly/deployment 
