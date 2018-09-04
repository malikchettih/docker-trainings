# docker-trainings

## Ubuntu 18.04 - Docker installation scripts

To install docker-ce to Unbuntu 18.04 workstation execute the folowing scripts
```
sudo apt-get update

sudo apt-get --yes install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

sudo apt-get update

sudo apt-get --yes install docker-ce   

```
To execute docker commands withour sudo, add the current user to the docker group
```
sudo usermod -aG docker $USER
```
