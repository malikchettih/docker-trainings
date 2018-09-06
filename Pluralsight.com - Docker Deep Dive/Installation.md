# Docker Installation

## Get Docker CE for ubuntu

Follow the procedure documented in https://docs.docker.com/install/linux/docker-ce/ubuntu/

```
sudo apt-get update

sudo apt-get install --yes \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository --yes \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"    

sudo apt-get update

sudo apt-get install docker-ce

```

## Optional Linux Post-Installation

### Manage Docker as a non-root user

Follow the procedure documented in https://docs.docker.com/install/linux/linux-postinstall/

```
sudo usermod -aG docker $USER
```
