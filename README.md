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



