# Run Django application as Container
# Explaination:
1. Django is a free and open-source, Python-based web framework for backend web applications
(https://docs.djangoproject.com/en/4.2/intro/install/)
2. Django requires python to be installed, so we will accordingly write dockerfile
3. you can create a Django skeleton project using below commands
    `django-admin startproject mysite` # mysite can be any name
4. The above command will create a project structure with some files
5. check if the project works by exposing the port 
    `$ python manage.py runserver 8080` or 
6. If you want to have ip address along with port , you can give following
    `python manage.py runserver 0.0.0.0:8000`

   
# Task1 : To create a simple Django project and check if application running  and then create dockerfile to run it as container
`Execute commands one by one on your local machine/ terminal first:`
```
    $ brew install python
    $ pip3 install Django 
    $ python3
    >>> import django
    >>> print(django.get_version()) # to check version or you can directly check on terminal after exit
    >>> exit()
    $ python3 -m django --version 
    $ django-admin startproject django_web_container 

( # Now you will see a outer folder django_web_container [you can change the name if you get confused] and it includes 'django_web_container'  and a 'manage.py'     
# by now you have just created the project, # It's time now to create a application and host it )

    $ python manage.py runserver # it will give the output with local ip address and bydefault runs on port 8000

    $ python manage.py runserver 0.0.0.0:8000 # if you want to change the ip address and port

```
# Run the project as container , commands to be executed are 
    1. docker build -t cloudhelp/task1-django-sampleweb:latest
    2. docker run -p 1234:8000 -it cloudhelp/task1-django-sampleweb: latest (or you can copy the image id instead this long image name)
    3. As docker is running on host, you can't access the webapplication outside its network, hence we need to expose the network by port mapping


# Task2 : To create a simple Django project but lets host our own application

`Execute commands one by one on your local machine/ terminal first:`

django-admin startproject django_web_container 




# Additional Info: 
```
`manage.py` -> is a command line utility that helps to interacts django project
`django_web_container` -> inside folder is the actual django project
`__init__.py` -> its a blank file that is must for any python project to run as thats a python package
`settings.py` -> is the high level project setting file, you can change the file
`urls.py` -> you can add the endpoints/urls here for an application
`wsgi.py` -> this is a webserver gateway file (we aren't going to make any changes to this file)
```

