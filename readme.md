# Install node in docker container

It is install from official web site https://nodejs.org
For example, I install version node v0.10.35
I use material 
* How to install Node.js via binary archive on Linux? (https://github.com/nodejs/help/wiki/Installation)
* Distributives (https://nodejs.org/dist/)

#### Dockerfile

```dockerfile
FROM ubuntu:16.04

#Install node 0.10.35 from https://nodejs.org/dist/v0.10.35/

RUN apt-get update && apt-get install -y wget tar
RUN mkdir /usr/local/lib/nodejs
RUN wget https://nodejs.org/dist/v0.10.35/node-v0.10.35-linux-x64.tar.gz
RUN tar -xvf node-v0.10.35-linux-x64.tar.gz -C /usr/local/lib/nodejs
RUN mv /usr/local/lib/nodejs/node-v0.10.35-linux-x64 /usr/local/lib/nodejs/node-v0.10.35
ENV NODEJS_HOME /usr/local/lib/nodejs/node-v0.10.35
ENV PATH $NODEJS_HOME/bin:$PATH
RUN node -v
RUN npm -v

# Test

RUN mkdir test
RUN cd test && echo "console.log('Hello, It is test for nodejs') \n \
             var a = 5; \n \
             console.log(a+1);">test.js
CMD node -v && cd test && node test.js

```

#### For run

```bash
$ sudo docker build -f Dockerfile.node10 -t node .
$ sudo docker run node
```

