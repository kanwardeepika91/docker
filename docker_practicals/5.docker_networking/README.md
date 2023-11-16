Few usecases where we need network concepts

1. container C1 or C2 should communicate with Host network  # can be achieved using bridge and host network
2. container C1 --> commmunicates with --> container C2  # can be achieved using bridge network
3. container C1 --> shouldn't commmunicates with --> container C2 # can be achieved using custom bridge network

## Bridge Network:
Whenever you create a container on the host, a Virtualnetwork (veth, docker0) between host and container is created bydefault which is known as Bridge Network
If you create multiple containers also, the docker0 virtual network is going to be same, so single virtual network for multiple containers (security concern) as C1 can ping C2 and vice-versa as i may want C1 and C2 to be isolated completely.
But, if the requirement is that C1 can talk to C2, then this network can be used.

## custom Bridge Network: 

## Host Network:
Containers would use the host network, in this case the docker will directly bind the network of host system to container (under same host CIDR block- this is networking concept) -     eth0 of your host
example: if eth0 of host is 192.16.18.23 then subnet of ip of docker maybe 192.16.18.33
so the container can ping the host and there won't be virtual network docker0 for this type of network 
Hence there is a security concern, as you want your contaners to be isolated to host network. 
## Overlay Network:



### Usage:  docker network COMMAND

Manage networks

Commands:
```
  connect     Connect a container to a network
  create      Create a network
  disconnect  Disconnect a container from a network
  inspect     Display detailed information on one or more networks
  ls          List networks
  prune       Remove all unused networks
  rm          Remove one or more networks
```

Run 'docker network COMMAND --help' for more information on a command.

