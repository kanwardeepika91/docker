# Run Django application as Container 

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

( # Now you will see a outer folder django_web_container [you can change the name if you get confused, i changed it to 'task1_django_web_container'] and it includes 'django_web_container'  and a 'manage.py'     
# by now you have just created the project, # It's time now to create a application and host it )

    $ python manage.py runserver # it will give the output with local ip address and bydefault runs on port 8000

    $ python manage.py runserver 0.0.0.0:8000 # if you want to change the ip address and port
```

# Task2 : To host the same above project in docker

### resusing the same task1 project to get idea what all files we gonna change when running project on docker container
1. A requirements.txt file is required for docker to run django project in container, so refer requirements.txt , better to create this file where manage.py exists"
    (this requirements.txt is just dependencies for django required to run in local)
2. Create a Dockerfile with all the steps required
3. docker build -t cloudhelp/task1-django-sampleweb:latest .
4. docker images (check your image is created)
5. docker run -it fdc8492158c6(imageid) # it will display 'Starting development server at http://0.0.0.0:8000/', you wont be able to access this server from your browser as its running inside the container. so expose the port 1234(host port):8080(docker container port) to the outside world, this is called `port mapping`
6. docker run -p 1234:8000 -it cloudhelp/task1-django-sampleweb:latest (or you can copy the image id instead this long image name)
7. As these tasks are done on Mac, try http://localhost:1234/, see localhost_django.png
8. If you run on Ec2 or any VM, then open 8000 port in Security Groups    


# Task3 : To create a simple Django project but lets host our own html application inside task3 folder
##### document: https://dockerize.io/guides/python-django-guide

`Execute commands one by one on your local machine/ terminal first:`

1. 'django-admin startproject django_html'  # create project django_html
2. create a requirements.txt file and place it where manage.py exists
3. 'python3 manage.py startapp hello_world' # create a hello_world app with
4. you will now see a new folder 'hello_wold' app with views.py and other files
5. Once you’ve created the app, you need to install it in your project. In django_html/settings.py, add the following line of code under INSTALLED_APPS:'hello_world',

    ```
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'hello_world'                # add this line
    ]
    ```
    #####  That line of code means that your project now knows that the app you just created exists. The next step is to create a view so that you can display something to a user

6. Navigate to the 'views.py' file in the hello_world directory. There’s already a line of code in there that imports render(). Add the following code:

```
        from django.shortcuts import render

        def hello_world(request):
            return render(request, 'hello_world.html', {})
```
7. You’ve defined a view function called helloworld(). When this function is called, it will render an HTML file called hello_world.html. That file doesn’t exist yet, so let's create it. Create that directory and subsequently a file named helloworld.html inside it:

    `$ mkdir hello_world/templates/
     $ touch hello_world/templates/hello_world.html`

8. You’ve now created a function to handle your views and templates to display to the user. The final step is to hook up your URLs so that you can visit the page you’ve just created. Your project has a module called urls.py in which you need to include a URL configuration for the hello_world app. Inside django_html/urls.py, add the following:

        `from django.contrib import admin
        from django.urls import path, include     # <--  ADD THIS LINE

        urlpatterns = [
            path('admin/', admin.site.urls),
            path('', include('hello_world.urls')),   # <--  ADD THIS LINE
        ]`

9.This looks for a module called urls.py inside the hello_world application and registers any URLs defined there. Whenever you visit the root path of your URL (localhost:8000), the hello_world application’s URLs will be registered. The hello_world.urls module doesn’t exist yet, so you’ll need to create it:

  $ touch hello_world/urls.py
  `     from django.urls import path
        from hello_world import views

        urlpatterns = [
            path('', views.hello_world, name='hello_world'),
        ]`
10. execute the command : python3 manage.py runserver 0.0.0.0:8000 and check 
(NOTE: If you want to access site at http://0.0.0.0:8000/, You may need to add '0.0.0.0' or ['*'] to ALLOWED_HOSTS in django_html/settings.py)
11. check image : django_hello_world_html.png
12. Lets dockerize the hello_world html page now
13.create a dockerfile , check dockerfile 
14.$ `docker build -t cloudhelp/django_html_hello_world .`
15. $ `docker images`
16. $ 'docker run -it -p 456:8000 9176dbcdba' # check image: 456_django_hello_world_html.png

## Additional Info: 
```
`manage.py` -> is a command line utility that helps to interacts django project
`django_web_container` -> A folder inside the task1_django_web_container is the actual django project
`__init__.py` -> its a blank file that is must for any python project to run as thats a python package
`settings.py` -> is the high level project setting file, you can change the file
`urls.py` -> you can add the endpoints/urls here for an application
`wsgi.py` -> this is a webserver gateway file (we aren't going to make any changes to this file)
```





