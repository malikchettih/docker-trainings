# Test web-app to use with Pluralsight courses and Docker Deep Dive book
# Linux x64
FROM ubuntu:18.04
ENV http_proxy "http://10.41.254.251:8080"

LABEL maintainer="malik.chettih@gmail.com"

# Config Proxy in image
RUN export http_proxy=$http_proxy
RUN export https_proxy=$http_proxy

# Get Back Sudo in the image
RUN apt-get update && apt-get install -y sudo && rm -rf /var/lib/apt/lists/*

# Install Node and NPM
RUN apt-get update
RUN apt-get install --yes curl
#RUN curl --silent --location https://deb.nodesource.com/setup_10.x | sudo -E bash -
RUN apt-get install --yes nodejs
RUN apt-get install --yes build-essential
RUN apt-get install --yes npm

# Copy app to /src
COPY . /src

WORKDIR /src

# NPM: Configure and update npm
RUN  npm config set strict-ssl false
RUN  npm config set registry "http://registry.npmjs.org/"
RUN  npm config set proxy $http_proxy
RUN  npm config set https-proxy $http_proxy
RUN  npm install npm --global

# NPM: Install dependencies
RUN  npm install

EXPOSE 8080

ENTRYPOINT ["node", "./app.js"]
