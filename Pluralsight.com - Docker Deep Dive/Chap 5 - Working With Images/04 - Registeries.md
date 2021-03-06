# Docker Registeries

# Image id in docker.io registery

An image is defined by REGISTERY_ID/IMAGE_NAME:IMAGE_VERSION.
* Registery is by default **docker.io**.
* Version is by default **latest**.

```
mchettih@ubuntu:~$ docker image pull docker.io/redis:latest
latest: Pulling from library/redis
Digest: sha256:858b1677143e9f8455821881115e276f6177221de1c663d0abef9b2fda02d065
Status: Image is up to date for redis:latest
```

To pull a specific image
```
mchettih@ubuntu:~$ docker image pull docker.io/redis:4.0.1
4.0.1: Pulling from library/redis
065132d9f705: Pull complete
be9835c27852: Pull complete
f4a0d1212c38: Pull complete
ea1f878b621a: Pull complete
7a838393b4b9: Pull complete
9f48e489da12: Pull complete
Digest: sha256:8a54dcc711406447b3631a81ef929f500e6836b43e7d61005fa27057882159da
Status: Downloaded newer image for redis:4.0.1
```

## Pull all Images
```
mchettih@ubuntu:~$ docker image pull docker.io/redis -a
2-32bit: Pulling from library/redis
51f5c6a04d83: Pull complete
6c8ccd839b1d: Pull complete
0fded1c9651d: Pull complete
7f1aa6a73799: Pull complete
61bd41cc96da: Pull complete
087610a7f646: Pull complete
4747742746f7: Pull complete
574d663436a1: Pull complete
d90e8a92b548: Pull complete
Digest: sha256:35201a22e6690d442ec1a3fdd6e640bf4441926d9c02ecaeb3f648869594449c
2.6-32bit: Pulling from library/redis
d4bce7fd68df: Pull complete
a3ed95caeb02: Pull complete
f19cce48c5a8: Pull complete
564ee6d16a2e: Pull complete
a251e59b24e2: Pull complete
df7f78e810e7: Pull complete
b085a9629ef4: Pull complete
2064e34931e2: Pull complete
d56ed431390d: Pull complete
Digest: sha256:bbc7a3f61125aedfc27ffd7c679147443cf7f5fc2a591bd60fbf7bf34dc71866
2.6.17-32bit: Pulling from library/redis
d4bce7fd68df: Already exists
a3ed95caeb02: Already exists
f19cce48c5a8: Already exists
564ee6d16a2e: Already exists
a251e59b24e2: Already exists
df7f78e810e7: Already exists
b085a9629ef4: Already exists
2064e34931e2: Already exists
d56ed431390d: Already exists
Digest: sha256:00eeb874fc1db19d34e67f6567f86a7626742a9269577352d91a43e4532a371f
2.6.17: Pulling from library/redis
d4bce7fd68df: Already exists
a3ed95caeb02: Pull complete
f19cce48c5a8: Already exists
f8b14ad54699: Pull complete
1cf40bdbfe7b: Pull complete
345507085de1: Pull complete
ae2c2b539a04: Pull complete
8b6eacdaf40a: Pull complete
2a13df011fbc: Pull complete
Digest: sha256:ef3e064323c58d74ddc71426be5aefd9d397b663bc6422abacc2f37821cc04b4
2.6: Pulling from library/redis
d4bce7fd68df: Already exists
a3ed95caeb02: Already exists
f19cce48c5a8: Already exists
f8b14ad54699: Already exists
1cf40bdbfe7b: Already exists
345507085de1: Already exists
ae2c2b539a04: Already exists
8b6eacdaf40a: Already exists
2a13df011fbc: Already exists
Digest: sha256:6c9f9cb9a250b12c15a92d8042a44f4557ca5bc590f36e63e529d52fb15b4ddc
2.8-32bit: Pulling from library/redis
Digest: sha256:35201a22e6690d442ec1a3fdd6e640bf4441926d9c02ecaeb3f648869594449c
2.8.10: Pulling from library/redis
a3ed95caeb02: Pull complete
7feb61e057c6: Pull complete
54301a7c2a89: Pull complete
85711e562c9a: Pull complete
493bcf01f4e8: Pull complete
b5c76ba3f46f: Pull complete
a7d59fc1be15: Pull complete
b20b0f77dbea: Pull complete
Digest: sha256:be7c7fe82b78bdc1c1e3249ac08e6eaca8e3d8d7fc3a77929d3b3eaec4c7ae42
2.8.11: Pulling from library/redis
a3ed95caeb02: Pull complete
7feb61e057c6: Already exists
54301a7c2a89: Already exists
85711e562c9a: Already exists
493bcf01f4e8: Already exists
1e28c1c2359a: Pull complete
c9d48101173c: Pull complete
b20b0f77dbea: Pull complete
Digest: sha256:effb926e6578c036aafe875562c9b87179cba12e385fcb94cb520c1c7f17c6d7
2.8.12: Pulling from library/redis
a3ed95caeb02: Pull complete
7feb61e057c6: Already exists
54301a7c2a89: Already exists
85711e562c9a: Already exists
493bcf01f4e8: Already exists
047f7be4fdc1: Pull complete
02a0e0cc9d21: Pull complete
b20b0f77dbea: Pull complete
Digest: sha256:6e36319eb459273cffa3a8b3bfab7c5dedaaac5a093478cc22954897e8ad57e7
2.8.13: Pulling from library/redis
a3ed95caeb02: Pull complete
7feb61e057c6: Already exists
54301a7c2a89: Already exists
85711e562c9a: Already exists
493bcf01f4e8: Already exists
7f42ea2231c9: Pull complete
225d20470f28: Pull complete
b20b0f77dbea: Pull complete
Digest: sha256:53c4202b7ced2864f1c850349e0e2960786e5e59c8b90cfc88d04207fc9e0689
2.8.14: Pulling from library/redis
a3ed95caeb02: Pull complete
7feb61e057c6: Already exists
54301a7c2a89: Already exists
85711e562c9a: Already exists
493bcf01f4e8: Already exists
b2553eb70550: Pull complete
d99e6501a26a: Pull complete
b20b0f77dbea: Pull complete
Digest: sha256:2c27a9acb5000a993b118921d181585c077b8810158e13dd2d3f03367df078fd
2.8.15: Pulling from library/redis
a3ed95caeb02: Pull complete
7feb61e057c6: Already exists
54301a7c2a89: Already exists
85711e562c9a: Already exists
493bcf01f4e8: Already exists
4f609d6b54af: Pull complete
64e8fc1f4eaf: Pull complete
b20b0f77dbea: Pull complete
Digest: sha256:65d4536e9dfe6e5410bcccd269a9f00291eeaf7b342c361c201b3d0b09f4e16a
2.8.16: Pulling from library/redis
a3ed95caeb02: Pull complete
7feb61e057c6: Already exists
54301a7c2a89: Already exists
85711e562c9a: Already exists
493bcf01f4e8: Already exists
0db37fac3203: Pull complete
4662f3f049c3: Pull complete
b20b0f77dbea: Pull complete
Digest: sha256:9ae8aa326a803c49064ae2c638d2c5a0e16245322327f723f2015ae16f925106
2.8.17: Pulling from library/redis
a3ed95caeb02: Pull complete
7feb61e057c6: Already exists
54301a7c2a89: Already exists
85711e562c9a: Already exists
cca4ac895fc5: Pull complete
518ca536473c: Pull complete
cbd4f7a1e52f: Pull complete
f0e420edb622: Pull complete
2a13df011fbc: Pull complete
Digest: sha256:a84ea9cb2974554b8e61cbb80160340a1873e066da49704afb81634f3df1c7cf
2.8.18: Pulling from library/redis
a3ed95caeb02: Pull complete
7feb61e057c6: Already exists
54301a7c2a89: Already exists
85711e562c9a: Already exists
cca4ac895fc5: Already exists
518ca536473c: Already exists
54f20bc4979f: Pull complete
f24da69bcd57: Pull complete
2a13df011fbc: Pull complete
Digest: sha256:05f7d664a7defc848cea6c9dcaa6093de2aea74cb4b3a3615ae3784ed5dbaa7e
2.8.19: Pulling from library/redis
193224d99eda: Pull complete
a3ed95caeb02: Pull complete
5d614b26c26f: Pull complete
8274a6625da0: Pull complete
86d9ae0920b7: Pull complete
f4f11f46a20e: Pull complete
dfff5f096b4a: Pull complete
70fa2e5ad71e: Pull complete
2a13df011fbc: Pull complete
Digest: sha256:990e1f57798f433364379cf2583702d843defb7630d8d1bb12dcdc6ce3d91ddb
2.8.20: Pulling from library/redis
6e69f355f70e: Pull complete
a3ed95caeb02: Pull complete
7d05668615e4: Pull complete
b4dd6d17b18d: Pull complete
2214d17f1f06: Pull complete
baf402c7f42b: Pull complete
62a217173c6e: Pull complete
9e987a1616af: Pull complete
2a13df011fbc: Pull complete
Digest: sha256:a6546e612f3023afeb5ab86ecffffa546c1e5ac30393469ac34f2f3915aaf0e1
2.8.21-32bit: Pulling from library/redis
80ab95908a2b: Pull complete
a3ed95caeb02: Pull complete
47a0d79f89b9: Pull complete
be2e67160185: Pull complete
fc7086ecaf68: Pull complete
ad0158c1e052: Pull complete
69fead57b0bb: Pull complete
832bca789dbc: Pull complete
d56ed431390d: Pull complete
Digest: sha256:8bbc973d45cfbe588d6ee18f8dd00ec84c794eacee614fd00765b5144e2d3962
2.8.21: Pulling from library/redis
80ab95908a2b: Already exists
a3ed95caeb02: Pull complete
47a0d79f89b9: Already exists
7190081b1686: Pull complete
fe09c22d81ac: Pull complete
a5eae2bcc645: Pull complete
db5d902d2396: Pull complete
027d6925890b: Pull complete
2a13df011fbc: Pull complete
Digest: sha256:13242146d50c76f402f7c2db7b37e74ca43914d28e928a767c3e62975bca4b99
2.8.22-32bit: Pulling from library/redis
8f47f7c36e43: Pull complete
a3ed95caeb02: Pull complete
bd51c4e1b5ac: Pull complete
bff59a9463d2: Pull complete
80011ff3a060: Pull complete
a11cc345112e: Pull complete
3c2c8871e2d8: Pull complete
071435521b0d: Pull complete
d56ed431390d: Pull complete
Digest: sha256:a793432e5fb73f7da6c628c92697a855d66c39c361bfe2f4fd7c95c32670aba0
2.8.22: Pulling from library/redis
8f47f7c36e43: Already exists
a3ed95caeb02: Pull complete
bd51c4e1b5ac: Already exists
77e4f61ab0ae: Pull complete
111feeb8cf13: Pull complete
d091c2f3053f: Pull complete
cc7d7e37fa96: Pull complete
166f1d6f8443: Pull complete
2a13df011fbc: Pull complete
Digest: sha256:b7984ede5c62746eff79f19ebc61851bcee99d5a7975b4198c4b1081e7d51621
2.8.23-32bit: Pulling from library/redis
Digest: sha256:35201a22e6690d442ec1a3fdd6e640bf4441926d9c02ecaeb3f648869594449c
2.8.23: Pulling from library/redis
51f5c6a04d83: Already exists
6c8ccd839b1d: Already exists
0fded1c9651d: Already exists
7f1aa6a73799: Already exists
fbe8a4f1aa87: Pull complete
1a9852d2edd3: Pull complete
128182e1e85d: Pull complete
b94de088b6d8: Pull complete
Digest: sha256:e507029ca6a11b85f8628ff16d7ff73ae54582f16fd757e64431f5ca6d27a13c
2.8.6: Pulling from library/redis
a3ed95caeb02: Pulling fs layer
7feb61e057c6: Already exists
54301a7c2a89: Already exists
85711e562c9a: Already exists
493bcf01f4e8: Already exists
e2b14019d3c3: Pulling fs layer
363913ac9bb0: Pulling fs layer
b20b0f77dbea: Waiting

mchettih@ubuntu:~$ docker image ls
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
malikchettih/get-started   part2               519c4e8dba2a        25 hours ago        132MB
redis                      latest              4e8db158f18d        3 weeks ago         83.4MB
python                     2.7-slim            40792d8a2d6d        4 weeks ago         120MB
hello-world                latest              2cb0d9787c4d        7 weeks ago         1.85kB
redis                      4.0.1               aaf79d45ddb1        11 months ago       107MB
redis                      2-32bit             19865a7ae96c        2 years ago         203MB
redis                      2.8-32bit           19865a7ae96c        2 years ago         203MB
redis                      2.8.23-32bit        19865a7ae96c        2 years ago         203MB
redis                      2.8.23              481995377a04        2 years ago         186MB
redis                      2.6-32bit           62b0a5c3ea45        2 years ago         158MB
redis                      2.6.17-32bit        62b0a5c3ea45        2 years ago         158MB
redis                      2.6                 a081f7d44c38        2 years ago         150MB
redis                      2.6.17              a081f7d44c38        2 years ago         150MB
redis                      2.8.22-32bit        b6353e3bb411        2 years ago         116MB
redis                      2.8.22              eaa6aada6f42        2 years ago         109MB
redis                      2.8.21-32bit        6f2b6a4332f1        3 years ago         116MB
redis                      2.8.21              fb83b0b93a51        3 years ago         109MB
redis                      2.8.20              992c435ae08c        3 years ago         111MB
redis                      2.8.19              dd9fe7db5236        3 years ago         111MB
redis                      2.8.18              5f9a9a936de2        3 years ago         111MB
redis                      2.8.17              01aaba7226f1        3 years ago         111MB
redis                      2.8.16              8b6103fd7b3e        3 years ago         111MB
redis                      2.8.15              dbb560009c50        3 years ago         111MB
redis                      2.8.14              4aad650df84a        3 years ago         111MB
redis                      2.8.13              c4f8a05f3aff        3 years ago         111MB
redis                      2.8.12              98bc726ecd17        3 years ago         111MB
redis                      2.8.11              2fb854cb3f76        3 years ago         111MB
redis                      2.8.10              33fe9dbeb30c        3 years ago         111MB
```
