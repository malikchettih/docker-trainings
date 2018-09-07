# Network Services

There are 2 main services :
1. Service Discovery : it all about locating a service in the swarm.
2. Load Balancing: access the service from any node of the swarm, even the one that are not hosting the service.

First let's clean all the services
```
mchettih@docker-instance-1:~$ docker service rm $(docker service ls -q)
whi10a3bld0e
```
## Service Discovery

Let's create 2 docker Services, ping and pong
```
mchettih@docker-instance-1:~$ docker network create -d overlay overnet
zjhhs0c9jbdq71hcesdn74cdt
```
```
mchettih@docker-instance-1:~$ docker service create -d --name ping --network overnet --replicas 3 alpine sleep 1d
d7m2349kpe2366xa95iyvg1o2
```
```
mchettih@docker-instance-1:~$ docker service create -d --name pong --network overnet --replicas 3 alpine sleep 1d
wd3ts3w8uguebfuci3ma0ztkk
```
```
mchettih@docker-instance-1:~$ docker service ls
ID                  NAME                MODE                REPLICAS            IMAGE               PORTS
d7m2349kpe23        ping                replicated          3/3                 alpine:latest
wd3ts3w8ugue        pong                replicated          3/3                 alpine:latest
```
```
mchettih@docker-instance-1:~$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
e9bfe69fc8a0        alpine:latest       "sleep 1d"          25 seconds ago      Up 23 seconds                           pong.2.gsd7lwilsn3b5ox1056i8xdx8
83806a817c3a        alpine:latest       "sleep 1d"          36 seconds ago      Up 32 seconds                           ping.2.vkq2b6rhjjfinic1c4fzv4fyn
```

No we are able to ping the pong service within a container.
pong is the name of the service, we can ping it thanks to the Service Discovery service.
```
mchettih@docker-instance-1:~$ docker container exec -it e9 sh
/ # ping pong
PING pong (10.0.0.9): 56 data bytes
64 bytes from 10.0.0.9: seq=0 ttl=64 time=0.086 ms
64 bytes from 10.0.0.9: seq=1 ttl=64 time=0.091 ms
64 bytes from 10.0.0.9: seq=2 ttl=64 time=0.098 ms
64 bytes from 10.0.0.9: seq=3 ttl=64 time=0.056 ms
64 bytes from 10.0.0.9: seq=4 ttl=64 time=0.094 ms
64 bytes from 10.0.0.9: seq=5 ttl=64 time=0.060 ms
64 bytes from 10.0.0.9: seq=6 ttl=64 time=0.063 ms
^C
--- pong ping statistics ---
7 packets transmitted, 7 packets received, 0% packet loss
round-trip min/avg/max = 0.056/0.078/0.098 ms
/ #
```

## Load Balancing

Let's create a new service
```
mchettih@docker-instance-1:~$ docker service create -d --name web --network overnet --replicas 1 -p 80:80 nginx
udwpzo9uzttu5ht2lk3d390gl
```

We are mapping the internal port 80 to the external port 80. And because it is service it replicas to all the nodes.

so all the followig URL display the nginx welcome page
 * http://docker-instance-1.westeurope.cloudapp.azure.com/
 * http://docker-instance-2.westeurope.cloudapp.azure.com/
 * http://docker-instance-3.westeurope.cloudapp.azure.com/
 
