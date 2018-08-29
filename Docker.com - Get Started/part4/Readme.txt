------------------------------------------------------------------
 Install Docker-machine
 https://github.com/docker/machine/releases
 https://docs.docker.com/machine/install-machine/#install-machine-directly


 https://docs.docker.com/machine/overview/
 https://docs.docker.com/machine/install-machine/

------------------------------------------------------------------

base=https://github.com/docker/machine/releases/download/v0.15.0 &&
  curl -L $base/docker-machine-$(uname -s)-$(uname -m) >/tmp/docker-machine &&
  sudo install /tmp/docker-machine /usr/local/bin/docker-machine

------------------------------------------------------------------
 Install Oracle VirtualBox
 https://www.virtualbox.org/wiki/Linux_Downloads 0
 https://www.ostechnix.com/install-oracle-virtualbox-ubuntu-16-04-headless-server/
------------------------------------------------------------------

sudo nano /etc/apt/sources.list
add  deb http://download.virtualbox.org/virtualbox/debian bionic contrib

wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -

sudo apt update

sudo apt install virtualbox-5.2

sudo usermod -aG vboxusers mchettih

sudo systemctl status vboxdrv

wget https://download.virtualbox.org/virtualbox/5.2.18/Oracle_VM_VirtualBox_Extension_Pack-5.2.18.vbox-extpack

sudo VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-5.2.18.vbox-extpac



------------------------------------------------------------------
 Instructions on
 https://docs.docker.com/get-started/part4/#understanding-swarm-clusters
------------------------------------------------------------------

Download https://github.com/boot2docker/boot2docker/releases/download/v18.06.1-ce/boot2docker.iso
cp ./Downloads/boot2docker.iso /home/mchettih/.docker/machine/cache/


IMPORTANT : sudo ifconfig vboxnet0 down && sudo ifconfig vboxnet0 up
Otherwise docker machines will not be reachable.


mchettih@ubuntu:~$ docker-machine create -d virtualbox     --engine-env HTTP_PROXY="http://mchettih:2408Nael%21%21201514@10.41.254.251:8080"     --engine-env HTTPS_PROXY="http://mchettih:2408Nael%21%21201514@10.41.254.251:8080"     --engine-env NO_PROXY="localhost,127.0.0.0/8,::1"     myvm1

Running pre-create checks...
(myvm1) Unable to get the latest Boot2Docker ISO release version:  Get https://api.github.com/repos/boot2docker/boot2docker/releases/latest: proxyconnect tcp: EOF
Creating machine...
(myvm1) Unable to get the latest Boot2Docker ISO release version:  Get https://api.github.com/repos/boot2docker/boot2docker/releases/latest: proxyconnect tcp: EOF
(myvm1) Copying /home/mchettih/.docker/machine/cache/boot2docker.iso to /home/mchettih/.docker/machine/machines/myvm1/boot2docker.iso...
(myvm1) Creating VirtualBox VM...
(myvm1) Creating SSH key...
(myvm1) Starting the VM...
(myvm1) Check network to re-create if needed...
(myvm1) Waiting for an IP...
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with boot2docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env myvm1



mchettih@ubuntu:~$ docker-machine create --driver virtualbox myvm2
Running pre-create checks...
(myvm2) Unable to get the latest Boot2Docker ISO release version:  Get https://api.github.com/repos/boot2docker/boot2docker/releases/latest: proxyconnect tcp: EOF
Creating machine...
(myvm2) Unable to get the latest Boot2Docker ISO release version:  Get https://api.github.com/repos/boot2docker/boot2docker/releases/latest: proxyconnect tcp: EOF
(myvm2) Copying /home/mchettih/.docker/machine/cache/boot2docker.iso to /home/mchettih/.docker/machine/machines/myvm2/boot2docker.iso...
(myvm2) Creating VirtualBox VM...
(myvm2) Creating SSH key...
(myvm2) Starting the VM...
(myvm2) Check network to re-create if needed...
(myvm2) Waiting for an IP...
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with boot2docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env myvm2


mchettih@ubuntu:~$ docker-machine ls
NAME    ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER        ERRORS
myvm1   -        virtualbox   Running   tcp://192.168.99.100:2376           v18.06.1-ce
myvm2   -        virtualbox   Running   tcp://192.168.99.101:2376           v18.06.1-ce


mchettih@ubuntu:~$ docker-machine ssh myvm1 "docker swarm init --advertise-addr 192.168.99.100"
Swarm initialized: current node (reujz5y5qgptcmco3lo113vjz) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-0ccm8xpu37eqoxbdod8511u0l3ii0aigsffrc3jraktklhg5e2-1emc633n5u5ksxh7t7z7v7910 192.168.99.100:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.



mchettih@ubuntu:~$ docker-machine ssh myvm2 "docker swarm join --token SWMTKN-1-0ccm8xpu37eqoxbdod8511u0l3ii0aigsffrc3jraktklhg5e2-1emc633n5u5ksxh7t7z7v7910 192.168.99.100:2377"
This node joined a swarm as a worker.


https://docs.docker.com/machine/reference/env/#excluding-the-created-machine-from-proxies

mchettih@ubuntu:~$ docker-machine env -no-proxy myvm1
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://192.168.99.100:2376"
export DOCKER_CERT_PATH="/home/mchettih/.docker/machine/machines/myvm1"
export DOCKER_MACHINE_NAME="myvm1"
export no_proxy="localhost,127.0.0.0/8,::1,192.168.99.100"
# Run this command to configure your shell:
# eval $(docker-machine env -no-proxy myvm1)

mchettih@ubuntu:~$ eval $(docker-machine env myvm1)


mchettih@ubuntu:~$ docker-machine ls
NAME    ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER        ERRORS
myvm1   *        virtualbox   Running   tcp://192.168.99.100:2376           v18.06.1-ce
myvm2   -        virtualbox   Running   tcp://192.168.99.101:2376           v18.06.1-ce
