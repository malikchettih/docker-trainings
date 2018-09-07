# Docker Network Types

## Docker Networks

Docker needs to be in swarm mode. 3 nodes in manager mode.
```
mchettih@docker-instance-2:~$ docker node ls
ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS      ENGINE VERSION
w5wn867dx5k9roqcg66d7no6u     docker-instance-1   Ready               Active              Leader              18.06.1-ce
z7i8o9ye18n027c2bf7mt2y7u *   docker-instance-2   Ready               Active              Reachable           18.06.1-ce
jsa2w9jxgg0h6cpxfunp4xd3s     docker-instance-3   Down                Active              Unreachable         18.06.1-ce
```

Listing docker networks
```
mchettih@docker-instance-1:~$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
4b4c465d5250        bridge              bridge              local
76920d17dda5        docker_gwbridge     bridge              local
0f2828a5b3eb        host                host                local
vyvw0cwo59cc        ingress             overlay             swarm
f9fc51bab938        none                null                local
```

default network driver is bridge. bridge is called nat on windows.

lets start a container.
```
mchettih@docker-instance-1:~$ docker container run --rm -d alpine sleep 1d
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
8e3ba11ec2a2: Pull complete
Digest: sha256:7043076348bf5040220df6ad703798fd8593a0918d06d3ce30c6c93be117e430
Status: Downloaded newer image for alpine:latest
6b6e7889e035ab091f8243a2340e607a173c3292c52e77b91d0bf00916c8f4a6
```
1. alpine image is pulled first. latest one.
2. alpine image is run in detached mode.

lets inspect the gridge network
```
mchettih@docker-instance-1:~$ docker network inspect bridge
[
    {
        "Name": "bridge",
        "Id": "4b4c465d52502117ceaa9fe5bdcfca9032d241af2d631d98f9ea12247ecc1023",
        "Created": "2018-09-06T07:06:46.6522252Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16",
                    "Gateway": "172.17.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "6b6e7889e035ab091f8243a2340e607a173c3292c52e77b91d0bf00916c8f4a6": {
                "Name": "gallant_jones",
                "EndpointID": "9dc1328796b15fc60931f0b817cd994151432555e96f3bf6b396c5877742b571",
                "MacAddress": "02:42:ac:11:00:02",
                "IPv4Address": "172.17.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]
```
Now we've got a container in the brige section:
```
"Containers": {
    "6b6e7889e035ab091f8243a2340e607a173c3292c52e77b91d0bf00916c8f4a6": {
        "Name": "gallant_jones",
        "EndpointID": "9dc1328796b15fc60931f0b817cd994151432555e96f3bf6b396c5877742b571",
        "MacAddress": "02:42:ac:11:00:02",
        "IPv4Address": "172.17.0.2/16",
        "IPv6Address": ""
    }
},
```


## Container Ports mapping

Lets start an nginx and map port 80 inside the container with port 80 outside the container.
```
mchettih@docker-instance-1:~$ docker container run --rm -d --name web -p 80:80 nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
802b00ed6f79: Pull complete
e9d0e0ea682b: Pull complete
d8b7092b9221: Pull complete
Digest: sha256:24a0c4b4a4c0eb97a1aabb8e29f18e917d05abfe1b7a7c07857230879ce7d3d3
Status: Downloaded newer image for nginx:latest
5d965c050aed5f9389593140c0ee1529827024aab362904cad7a024f6b0899d7
```

To check port mapping for web container
```
mchettih@docker-instance-1:~$ docker port web
80/tcp -> 0.0.0.0:80
```

## Create Docker networks

To create a new network given a specific DRIVER (bridge)
```
mchettih@docker-instance-1:~$ docker network create -d bridge golden-gate
0d1f055dca840ed1490c32af1ed6a448b6e20d0a579ccd20f3954b8eda70e638
```
golden-gate network was created
```
mchettih@docker-instance-1:~$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
4b4c465d5250        bridge              bridge              local
76920d17dda5        docker_gwbridge     bridge              local
0d1f055dca84        golden-gate         bridge              local
0f2828a5b3eb        host                host                local
vyvw0cwo59cc        ingress             overlay             swarm
f9fc51bab938        none                null                local
```

To start a container within a network
```
mchettih@docker-instance-1:~$ docker container run --rm -d --network golden-gate alpine sleep 1d
46464a1d0fe496409b5f7b1b8cededd4f5a9ac8a84b65a1fe401f518e56f25ea
```

## Create Docker Overlay networks

To create a network with overlay driver we need docker in swarm mode.

```
mchettih@docker-instance-1:~$ docker network create -d overlay overnet
x3gumaf2hk5p9ja07j2o5cssi
```

```
mchettih@docker-instance-1:~$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
4b4c465d5250        bridge              bridge              local
76920d17dda5        docker_gwbridge     bridge              local
0d1f055dca84        golden-gate         bridge              local
0f2828a5b3eb        host                host                local
vyvw0cwo59cc        ingress             overlay             swarm
f9fc51bab938        none                null                local
x3gumaf2hk5p        overnet             overlay             swarm
```

The overnet network was created with driver overlay and scope swarm. That means that it is available on evry node of the swarm.

Now let's start a service called pinger replicated twice on the overnet network
```
mchettih@docker-instance-1:~$ docker service create -d --name pinger --replicas 2 --network overnet alpine sleep 1d
whi10a3bld0eh01txtd0uw6ao
```
We've got to replicas, let's check on wich node they are one.
```
mchettih@docker-instance-1:~$ docker service ps pinger
ID                  NAME                IMAGE               NODE                DESIRED STATE       CURRENT STATE            ERROR               PORTS
n3eho50xn6w9        pinger.1            alpine:latest       docker-instance-3   Running             Running 14 seconds ago
4fyvd4jf1ya2        pinger.2            alpine:latest       docker-instance-1   Running             Running 20 seconds ago
```
We've got one task on docker-instance-1 node and the other on docker-instance-3. Let's list container on node docker-instance-1.
```
mchettih@docker-instance-1:~$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
cc6109573e19        alpine:latest       "sleep 1d"          3 minutes ago       Up 3 minutes                            pinger.2.4fyvd4jf1ya2w6jvkapkssb3k
```

We can open a bash command on the container. And ping the container on the docker-instance-3 nodes
```
mchettih@docker-instance-1:~$ docker container exec -it cc sh
/ # ifconfig
eth0      Link encap:Ethernet  HWaddr 02:42:0A:00:00:06
          inet addr:10.0.0.6  Bcast:10.0.0.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1450  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

eth1      Link encap:Ethernet  HWaddr 02:42:AC:12:00:03
          inet addr:172.18.0.3  Bcast:172.18.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:11 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:866 (866.0 B)  TX bytes:0 (0.0 B)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

/ # ping 10.0.0.7
PING 10.0.0.7 (10.0.0.7): 56 data bytes
64 bytes from 10.0.0.7: seq=0 ttl=64 time=0.693 ms
64 bytes from 10.0.0.7: seq=1 ttl=64 time=0.424 ms
64 bytes from 10.0.0.7: seq=2 ttl=64 time=0.996 ms
64 bytes from 10.0.0.7: seq=3 ttl=64 time=0.618 ms
64 bytes from 10.0.0.7: seq=4 ttl=64 time=0.631 ms
^C
--- 10.0.0.7 ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max = 0.424/0.672/0.996 ms
/ #
```

Same thing from the docker-instance-3, we can open bash command on the container in this node and then ping the container in the node docker-instance-1

```
mchettih@docker-instance-3:~$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS              PORTS               NAMES
c0f2aa42a4da        alpine:latest       "sleep 1d"          About a minute ago   Up About a minute                       pinger.1.n3eho50xn6w9ip4s3dnomvlq9

mchettih@docker-instance-3:~$ docker container exec -it c0 sh
/ # ifconfig
eth0      Link encap:Ethernet  HWaddr 02:42:0A:00:00:07
          inet addr:10.0.0.7  Bcast:10.0.0.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1450  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

eth1      Link encap:Ethernet  HWaddr 02:42:AC:12:00:03
          inet addr:172.18.0.3  Bcast:172.18.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:11 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:866 (866.0 B)  TX bytes:0 (0.0 B)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

/ # ping 10.0.0.6
PING 10.0.0.6 (10.0.0.6): 56 data bytes
64 bytes from 10.0.0.6: seq=0 ttl=64 time=0.681 ms
64 bytes from 10.0.0.6: seq=1 ttl=64 time=0.707 ms
64 bytes from 10.0.0.6: seq=2 ttl=64 time=0.477 ms
64 bytes from 10.0.0.6: seq=3 ttl=64 time=0.598 ms
64 bytes from 10.0.0.6: seq=4 ttl=64 time=0.923 ms
64 bytes from 10.0.0.6: seq=5 ttl=64 time=0.605 ms
64 bytes from 10.0.0.6: seq=6 ttl=64 time=0.579 ms
64 bytes from 10.0.0.6: seq=7 ttl=64 time=0.607 ms
64 bytes from 10.0.0.6: seq=8 ttl=64 time=0.866 ms
^C
--- 10.0.0.6 ping statistics ---
9 packets transmitted, 9 packets received, 0% packet loss
round-trip min/avg/max = 0.477/0.671/0.923 ms
/ #

```
