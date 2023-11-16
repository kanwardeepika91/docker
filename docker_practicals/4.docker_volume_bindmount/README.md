# Bind mount 
 1. you can mount the container folder to host mount point, so that data will be persistent even if docker crashes
 2. data will be stored in the host mount folder
 ### Limitation:
 1. Bind mount is specific to its host, meaning you cannot mount that folder to any other host
 2. you can manage it using docker cli commands 

# volume 
1. its a logical volume, it works as lifecycle - you can create/destroy volume, you can mount to another containers also
2. you can mount volume to any other hosts/other external ec2 instance/s3/nfs etc, this way taking backup and attaching to any of the services becomes easy
3. high performace as they can be external services attach to volume

### Usage:  docker volume COMMAND

Manage volumes Commands:
```
  create      Create a volume
  inspect     Display detailed information on one or more volumes
  ls          List volumes
  prune       Remove unused local volumes
  rm          Remove one or more volumes
```
Run 'docker volume COMMAND --help' for more information on a command

### Docker mount commands: 
 source is your local host where you created volume, target is the folder inside container
1. docker run -d --mount source=deepika,target=/app imageid
2. docker ps
3. docker inspect containerid (you can get all the details of container, you can also check Mounts section)

## Docker volume creation and deletion:
1. docker volume create deepika

If you want to delete the volume, you need to stop the container, else you can't as that volume will be in-use to container
1. docker stop containerid
2. docker volume rm deepika



 
