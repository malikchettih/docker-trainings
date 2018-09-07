# Attaching Volumes to Containers

# Attach a new volume to a Container

We run a new container and attach to it a volume named ubervol.
If ubervol does not exists, it will create it.
```
mchettih@docker-instance-1:~$ docker container run -dit --name voltest --mount source=ubervol,target=/vol alpine:latest
ec932967ff5dfb83abbe636ad48cab6450984382489cd91a2b0e8d0b31b55e55
```

```
mchettih@docker-instance-1:~$ docker volume ls
DRIVER              VOLUME NAME
local               ubervol
mchettih@docker-instance-1:~$ sudo ls -l /var/lib/docker/volumes
total 28
-rw------- 1 root root 32768 Sep  7 08:33 metadata.db
drwxr-xr-x 3 root root  4096 Sep  7 08:33 ubervol
```

The ubervol volume is mounted to the /vol directory in the container.

```
mchettih@docker-instance-1:~$ docker container exec -it voltest sh
/ # ls
bin    dev    etc    home   lib    media  mnt    proc   root   run    sbin   srv    sys    tmp    usr    var    vol
/ # ls /vol
/ # cd vol
/vol # echo "some data" >> ./newfile
/vol # cat ./newfile
some data
/vol # exit
```

Data are stored in the volume and are persistent.
```
mchettih@docker-instance-1:~$ sudo cat /var/lib/docker/volumes/ubervol/_data/newfile
some data
```
