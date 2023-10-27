# create a docker hub account 
(https://hub.docker.com/)

# commands to create image and run container:
    `1. docker build -t dockerhubaccount-username/name-of-image:latest .`  
        # to build a image using dockerfile where dockerfile is in current location
        # if dockerfile is in another location, give that path or use command as below:
    `1a. docker build -t dockerhubaccount-username/name-of-image:latest /helloworld/dockerfile`
    `Example: docker build -t cloudhelp/python-sample-docker:latest .`
        # -t means giving a tag name to image
    `2. docker run -it dockerhubaccount-username/name-of-image:latest`
        # to run a container
     `3. docker images`
        # to check the images on the docker host
     `4. docker ps`
        # to check the containers running      

# commands to push or pull images from dockerhub /can be private registry account       
    `1. docker login` 
       # to login to docker hub account
    `2. docker push dockerhubaccount-username/name-of-image:latest`
        #  to push the image to dockerhub account
    `3. docker pull  dockerhubaccount-username/name-of-image:latest` 
        # to pull the image from dockerhub account  