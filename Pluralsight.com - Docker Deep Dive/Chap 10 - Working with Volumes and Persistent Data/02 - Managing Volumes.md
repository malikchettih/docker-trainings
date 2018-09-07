# Managing Docker Volumes
```
mchettih@docker-instance-1:~$ docker volume

Usage:  docker volume COMMAND

Manage volumes

Commands:
  create      Create a volume
  inspect     Display detailed information on one or more volumes
  ls          List volumes
  prune       Remove all unused local volumes
  rm          Remove one or more volumes

Run 'docker volume COMMAND --help' for more information on a command.
```

## Create a VOLUME
```
mchettih@docker-instance-1:~$ docker volume create vol1
vol1
mchettih@docker-instance-1:~$ docker volume create vol2
vol2
mchettih@docker-instance-1:~$ docker volume ls
DRIVER              VOLUME NAME
local               vol1
local               vol2
```

## Inspect a Volume
```
mchettih@docker-instance-1:~$ docker volume inspect vol1
[
    {
        "CreatedAt": "2018-09-07T08:18:31Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/vol1/_data",
        "Name": "vol1",
        "Options": {},
        "Scope": "local"
    }
]
```
```
mchettih@docker-instance-1:~$ sudo ls /var/lib/docker/volumes -all
total 40
drwx------  4 root root  4096 Sep  7 08:23 .
drwx--x--x 15 root root  4096 Sep  7 07:58 ..
-rw-------  1 root root 32768 Sep  7 08:23 metadata.db
drwxr-xr-x  3 root root  4096 Sep  7 08:18 vol1
drwxr-xr-x  3 root root  4096 Sep  7 08:23 vol2
```
Volumes are stored in /var/lib/docker/volumes

## Delete Volumes

```
mchettih@docker-instance-1:~$ docker volume rm vol1 vol2
vol1
vol2
```

Directories are deleted.
```
mchettih@docker-instance-1:~$ sudo ls /var/lib/docker/volumes -all
total 32
drwx------  2 root root  4096 Sep  7 08:25 .
drwx--x--x 15 root root  4096 Sep  7 07:58 ..
-rw-------  1 root root 32768 Sep  7 08:25 metadata.db
```
