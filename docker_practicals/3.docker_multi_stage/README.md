using Base image and other minimalistic image/python/distroless images which are very lightweight
Example1: If there is any application which requires only Java runtime, then we can prefer java base image which and its size maybe in mbs.
Example2: Incase, ubuntu and java both are required, but to build application - ubuntu required and for runtime java is required. then comes the multi stage concept
where you segregate the tasks of ubuntu and java and make java as final stage.
you can have multiple stages before, but final stage will only be created  to run as container which will be again lightweight
Final stage always gathers instructions from previous stages but removes all other stages.