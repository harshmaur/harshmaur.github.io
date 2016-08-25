---
layout: single
title: Minimal Setup to Get Started With Django on Ubuntu
modified:
categories:
excerpt: Getting started with Django on Ubuntu 14.04 with minimal setup and some useful tips and tricks to work your way around the project.
tags: [django, ubuntu]
image:
  feature:
date: 2016-03-10T12:58:00+05:30
comments: true
share: true
---

Installing and setting up Django can get very intimidating if you are just starting out with the framework.

[Django Official Documentation](https://docs.djangoproject.com/en/1.9/) is a very good place to start reading about Django. Make sure you are on the *correct* documentation version.

In this blog post I will guide you through the process of installing django and writing your first "Hello World!" application in your development environment with very minimal setup without getting into the specifics of installing web servers, virtualenv.

So Let's get started...

I am assuming that you already have python installed on your machines along with **python-pip**

In case you haven't run the following.

~~~ bash
sudo apt-get install python-pip
~~~

Let's install Django.

~~~~ bash
sudo pip install django
django-admin --version
~~~~

Now you will need to go into the directory where you want to start your project. I create my application projects inside the /projects/ directory in my User folder. However it can be anything you like.

~~~ bash
cd ~
mkdir projects && cd projects
django-admin startproject projectname # This will create a directory named "projectname" in the opt folder
~~~

The folder structure inside the **/projects/** direcotry should look like this.

~~~
.
`-- projectname
    |-- manage.py
    `-- projectname
        |-- __init__.py
        |-- settings.py
        |-- urls.py
        `-- wsgi.py
~~~

Incase you already created a folder inside the directory, you can also start the project without creating an additional folder inside it.

~~~ bash
django-admin startproject projectname . # Notice the trailing "dot"
~~~

There are two files that you need to know about here:

>**settings.py** : This is where all your configurations for your django project resides.
>**urls.py** : This file is for maintaining the routers of your web application.

We will look into both of these files soon.

Django by default uses a SQLite database by default(make sure it is installed on your machine). However if you would like to change the database to something else, you can follow the official guide [here](https://docs.djangoproject.com/en/1.9/ref/databases/)

*manage.py* in django gives a convinient way to manage the models you have in your application. To start off, lets sync our database with django and run the application to test it.  

~~~ bash
./manage.py migrate # make sure you are in the directory where manage.py is present.

Operations to perform:
  Apply all migrations: admin, contenttypes, auth, sessions
Running migrations:
  Rendering model states... DONE
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  .....

./manage.py runserver

Performing system checks...

System check identified no issues (0 silenced).
March 10, 2016 - 13:11:14
Django version 1.9.4, using settings 'projectname.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.

~~~

*In case you get OperationalError in django while performing migrate, it because your user does not have permissions to write the files in your current directory. Make sure that the django project is owned by your user.*

If you receive the output like above, that means you were able to run the server properly and the website will display "It Worked!" message.

Let's create a django app inside our project where we will code our first hello world! program and look into the views and the url routings.

~~~ bash
./manage.py startapp hello
~~~

Here, "hello" is the app name, however it can be anything you like.

The Structure of the whole project should now looks something like this.

~~~
.
`-- projectname
    |-- db.sqlite3
    |-- hello
    |   |-- admin.py
    |   |-- apps.py
    |   |-- __init__.py
    |   |-- migrations
    |   |   `-- __init__.py
    |   |-- models.py
    |   |-- tests.py
    |   `-- views.py
    |-- manage.py
    `-- projectname
        |-- __init__.py
        |-- __init__.pyc
        |-- settings.py
        |-- settings.pyc
        |-- urls.py
        |-- urls.pyc
        |-- wsgi.py
        `-- wsgi.pyc
~~~

You will notice quite a lot of new files now. The most important one to look for is views.py inside "hello" directory. We will also create urls.py inside the directory to map a function inside the view to a url which can be then rendered.

Let's open up views.py and enter the following code.

~~~ python
from django.shortcuts import render
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world!")
~~~

Now we are going to map "index" function with a url

~~~ bash
touch urls.py # this should be created inside "hello" directory
~~~

Open urls.py

~~~ python
from django.conf.urls import url

from . import views

urlpatterns = [
    url(r'^$', views.index, name='index'),
]
~~~

Next we have to include the hello.urls inside the root projectname/urls.py file.

~~~ bash
cd ..
cd projectname
vim urls.py # I use vim as my text editor, however you can use any editor of your choice.
~~~

In the *django.conf.urls* add another import of *include*

Then inside urlpatterns, include your hello.urls like this.

~~~ python
urlpatterns = [
    url(r'^', include('hello.urls')),
    url(r'^admin/', admin.site.urls),
]
~~~

Start your server if its not already running by *./manage.py runserver*

If you visit http://localhost:8000, you will see your hello world message coming up.

So, we are now done with the minimal setup with django.


### What's Next?

I recommend going through [Django Polls](https://docs.djangoproject.com/en/1.9/) and [Rango](http://www.tangowithdjango.com) to strengthen the basics of Django. The latter being a bit *outdated*, so a word of caution when following through the tutorial, however most of the things should work with the latest django versions. Django documentation is very well documented and most of the times all you have to do is open it up and solve your problems.

If you have any questions or you cannot get it to work, feel free to ask questions below. I would be eager to listen to you.
