## For your Additional information:
```
You may find that a requirements.txt file is required for any django project to run in container, well the below command i tried to get requirements.txt by 'pip3 freeze' but but I'm getting error. Hence as per one of the documentation, it is advised that whatever we import (when doing manually) add only those to requirements.txt file.

*Initial command i used to generate requirements.txt:*
A requirements.txt file is required for docker to run django project in container, so type the command in a directory where manage.py exists : "`pip3 freeze -l > requirements.txt`"
*Error1: OS Error*
ERROR: Could not install packages due to an OSError: [Errno 2] No such file or directory:'/home/users/anypath/'
```

Solution: Create requirements.txt manually ( you would know what all you have imported while creating a Django sample application)

*Error2: unable to delete the image* 
Error response from daemon: conflict: unable to remove repository reference "cloudhelp/task1-django-sampleweb" (must force) - container 4d9a2d24fa2f is using its referenced image 11ec1021ba91
Solutions: force to delete the image using below command
$ command: "`docker rmi -f cloudhelp/task1-django-sampleweb`"

Error3: If you can't still remove the image by using above commands
```
    mac:task2 sainath$ `docker rmi -f fdc8492158c6`
    Error response from daemon: conflict: unable to delete fdc8492158c6 (cannot be forced) - image is being used by running container dafbec663ade
    mac:task2 sainath$ `docker rm dafbec663ade`
    Error response from daemon: You cannot remove a running container dafbec663ade7763f73c8d3d0f53ad37131f449bc17d73f83c5f96be5ef6fec8. Stop the container before attempting removal or force remove
    mac:task2 sainath$ `docker stop dafbec663ade`
    dafbec663ade
    mac:task2 sainath$ `docker rm dafbec663ade`
    dafbec663ade
    mac:task2 sainath$ `docker rmi fdc8492158c6`
    Untagged: cloudhelp/task1-django-sampleweb:latest
    Deleted: sha256:fdc8492158c6449cba17c12a4a164d01e0e5304d890df4da72510809373f1aff
```

Error4: incase if you mention in dockerfile:  WORKDIR task3, it will give you below error 
mac:task3 sainath$ docker run -it db589c9064f0
python3: can't open file '/task3/manage.py': [Errno 2] No such file or directory