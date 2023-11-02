# Run Django application as Container 
# Explaination:
```
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
```

   
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

( # Now you will see a outer folder django_web_container [you can change the name if you get confused, i changed it to 'task1_django_web_container'] and it includes 'django_web_container'  and a 'manage.py'     
# by now you have just created the project, # It's time now to create a application and host it )

    $ python manage.py runserver # it will give the output with local ip address and bydefault runs on port 8000

    $ python manage.py runserver 0.0.0.0:8000 # if you want to change the ip address and port

```
# resusing the same task1 project to get idea what all files we gonna change when running project on docker container
# Run the project as container , commands to be executed are 
    1. A requirements.txt file is required for docker to run django project in container, so refer requirements.txt"
    (this requirements.txt is just dependencies for django required to run in local)
    2. Create a Dockerfile with all the steps required
    3. docker build -t cloudhelp/task1-django-sampleweb:latest .
    4. docker images (check your image is created)
    5. docker run -it fdc8492158c6(imageid) # it will display 'Starting development server at http://0.0.0.0:8000/', you wont be able to access this server from your browser as its running inside the container. so expose the port 1234(host port):8080(docker container port) to the outside world, this is called `port mapping`
    5. docker run -p 1234:8000 -it cloudhelp/task1-django-sampleweb:latest (or you can copy the image id instead this long image name)
    6. As these tasks are done on Mac, try http://localhost:1234/, see localhost_django.png
    7. If you run on Ec2 or any VM, then open 8000 port in Security Groups


# Task2 : To create a simple Django project but lets host our own application

`Execute commands one by one on your local machine/ terminal first:`

django-admin startproject django_web_container 





