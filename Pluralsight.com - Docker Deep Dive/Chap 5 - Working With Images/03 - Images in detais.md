# Docker Images in details

## Pull an Image
To pull an image from the docker hub repository. the following command request the to pull the latest redis image from docker hub
```
mchettih@ubuntu:~$ docker image pull redis
Using default tag: latest
latest: Pulling from library/redis
be8881be8156: Already exists
d6f5ea773ca3: Pull complete
735cc65c0db4: Pull complete
787dddf99946: Pull complete
0733799a7c0a: Pull complete
6d250f04811a: Pull complete
Digest: sha256:858b1677143e9f8455821881115e276f6177221de1c663d0abef9b2fda02d065
Status: Downloaded newer image for redis:latest
```

Pull Image is a 2 steps process:
get Manifest + pull layers

## List all Images
```
mchettih@ubuntu:~$ docker image ls
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
malikchettih/get-started   part2               519c4e8dba2a        25 hours ago        132MB
redis                      latest              4e8db158f18d        3 weeks ago         83.4MB
python                     2.7-slim            40792d8a2d6d        4 weeks ago         120MB
hello-world                latest              2cb0d9787c4d        7 weeks ago         1.85kB
```

## List all Images with digests
```
mchettih@ubuntu:~$ docker image ls  --digests
REPOSITORY                 TAG                 DIGEST                                                                    IMAGE ID            CREATED             SIZE
malikchettih/get-started   part2               sha256:4233b6f3647a423edabf40eb0fb43f6093a159581adeac5bec5647e1a1051a71   519c4e8dba2a        25 hours ago        132MB
redis                      latest              sha256:858b1677143e9f8455821881115e276f6177221de1c663d0abef9b2fda02d065   4e8db158f18d        3 weeks ago         83.4MB
python                     2.7-slim            sha256:447e3a799a60fa5c98b1e429f3f814fe55642b1a38099702720d8ae96e9eaeaf   40792d8a2d6d        4 weeks ago         120MB
hello-world                latest              sha256:4b8ff392a12ed9ea17784bd3c9a8b1fa3299cac44aca35a85c90c5e3c7afacdc   2cb0d9787c4d        7 weeks ago         1.85kB
```

## Show the history of an image
```
mchettih@ubuntu:/var/lib/docker$ docker history redis
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
4e8db158f18d        3 weeks ago         /bin/sh -c #(nop)  CMD ["redis-server"]         0B
<missing>           3 weeks ago         /bin/sh -c #(nop)  EXPOSE 6379/tcp              0B
<missing>           3 weeks ago         /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…   0B
<missing>           3 weeks ago         /bin/sh -c #(nop) COPY file:9c29fbe8374a97f9…   344B
<missing>           3 weeks ago         /bin/sh -c #(nop) WORKDIR /data                 0B
<missing>           3 weeks ago         /bin/sh -c #(nop)  VOLUME [/data]               0B
<missing>           3 weeks ago         /bin/sh -c mkdir /data && chown redis:redis …   0B
<missing>           3 weeks ago         /bin/sh -c set -ex;   buildDeps='   wget    …   24.8MB
<missing>           3 weeks ago         /bin/sh -c #(nop)  ENV REDIS_DOWNLOAD_SHA=fc…   0B
<missing>           3 weeks ago         /bin/sh -c #(nop)  ENV REDIS_DOWNLOAD_URL=ht…   0B
<missing>           3 weeks ago         /bin/sh -c #(nop)  ENV REDIS_VERSION=4.0.11     0B
<missing>           6 weeks ago         /bin/sh -c set -ex;   fetchDeps="   ca-certi…   3MB
<missing>           6 weeks ago         /bin/sh -c #(nop)  ENV GOSU_VERSION=1.10        0B
<missing>           6 weeks ago         /bin/sh -c groupadd -r redis && useradd -r -…   329kB
<missing>           6 weeks ago         /bin/sh -c #(nop)  CMD ["bash"]                 0B
<missing>           6 weeks ago         /bin/sh -c #(nop) ADD file:919939fa022472751…   55.3MB
```
## Inspect Low level iage information
```            
mchettih@ubuntu:/var/lib/docker$ docker inspect redis
[
    {
        "Id": "sha256:4e8db158f18dc71307f95260e532df39a9b604b51d4e697468e82845c50cfe28",
        "RepoTags": [
            "redis:latest"
        ],
        "RepoDigests": [
            "redis@sha256:858b1677143e9f8455821881115e276f6177221de1c663d0abef9b2fda02d065"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2018-08-04T02:40:22.380761478Z",
        "Container": "dea18b4bb2a3b201cc0164fc23fdae6b6cfe623dcc7117365993397821e2a678",
        "ContainerConfig": {
            "Hostname": "dea18b4bb2a3",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "6379/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "GOSU_VERSION=1.10",
                "REDIS_VERSION=4.0.11",
                "REDIS_DOWNLOAD_URL=http://download.redis.io/releases/redis-4.0.11.tar.gz",
                "REDIS_DOWNLOAD_SHA=fc53e73ae7586bcdacb4b63875d1ff04f68c5474c1ddeda78f00e5ae2eed1bbb"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "CMD [\"redis-server\"]"
            ],
            "ArgsEscaped": true,
            "Image": "sha256:18f382866d1d6cfee5e36ed403a77e11b21474221e27d23bef2aa412df1e3343",
            "Volumes": {
                "/data": {}
            },
            "WorkingDir": "/data",
            "Entrypoint": [
                "docker-entrypoint.sh"
            ],
            "OnBuild": [],
            "Labels": {}
        },
        "DockerVersion": "17.06.2-ce",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "6379/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "GOSU_VERSION=1.10",
                "REDIS_VERSION=4.0.11",
                "REDIS_DOWNLOAD_URL=http://download.redis.io/releases/redis-4.0.11.tar.gz",
                "REDIS_DOWNLOAD_SHA=fc53e73ae7586bcdacb4b63875d1ff04f68c5474c1ddeda78f00e5ae2eed1bbb"
            ],
            "Cmd": [
                "redis-server"
            ],
            "ArgsEscaped": true,
            "Image": "sha256:18f382866d1d6cfee5e36ed403a77e11b21474221e27d23bef2aa412df1e3343",
            "Volumes": {
                "/data": {}
            },
            "WorkingDir": "/data",
            "Entrypoint": [
                "docker-entrypoint.sh"
            ],
            "OnBuild": [],
            "Labels": null
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 83399992,
        "VirtualSize": 83399992,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/bfde350e294e379c67aa06bdd92180f4235baff175f6a38acb2ffb930a47eb01/diff:/var/lib/docker/overlay2/2b56bd3f19d18f1a464aca68d5c142ad0669f33bc63a716339060f5042f5c0b8/diff:/var/lib/docker/overlay2/3c82c37cca5f7010b0fe58282abd8744214677b4548196c28918b6706531fcf6/diff:/var/lib/docker/overlay2/8b3384d7602d416e0719d333337b2e277a0c74e0d51d1168d7a101840ffc196e/diff:/var/lib/docker/overlay2/121b7f7da519c0dd67daf73c897e341bdb62c46482a3f56946658df37afa75af/diff",
                "MergedDir": "/var/lib/docker/overlay2/6ba7f7a8d1942f2aeae05922ef4a08e799c4ba2c1a94a26e2b1700f345bd3c35/merged",
                "UpperDir": "/var/lib/docker/overlay2/6ba7f7a8d1942f2aeae05922ef4a08e799c4ba2c1a94a26e2b1700f345bd3c35/diff",
                "WorkDir": "/var/lib/docker/overlay2/6ba7f7a8d1942f2aeae05922ef4a08e799c4ba2c1a94a26e2b1700f345bd3c35/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:cdb3f9544e4c61d45da1ea44f7d92386639a052c620d1550376f22f5b46981af",
                "sha256:765d87ec3358c0e0f703a44e543193be2ae2cde89978a88f6a75ee616d22e05b",
                "sha256:54db18bc71ccff63f1bb2e080d7dd86aeec5f30bec02f82c3efa8499fc5bbd5e",
                "sha256:0c776a3ed24694e8611871d909bbee9fa5ef985dbf76a70b4becfa43e190f7d2",
                "sha256:7c04eaab6a330021b3b39a3ef27c7f04588f8adb5570e07ffc7a59d0fa3bee2b",
                "sha256:39deb50f842955103d3d67419a6779d19b35a34b5e96b8aed12d0d7ddd5c29e6"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]
```
