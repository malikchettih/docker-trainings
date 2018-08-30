# Test web-app to use with Pluralsight courses and Docker Deep Dive book
# Linux x64
FROM alpine

LABEL maintainer="malik.chettih@gmail.com"

# Install Node and NPM
RUN apk add --update nodejs nodejs-npm

# Copy app to /src
COPY . /src

WORKDIR /src

# Install dependencies
RUN  npm install
RUN  npm config set proxy http://mchettih:2408Nael%21%21201514@10.41.254.251:8080
RUN  npm config set https-proxy https://mchettih:2408Nael%21%21201514@10.41.254.251:8080

EXPOSE 8080

ENTRYPOINT ["node", "./app.js"]
