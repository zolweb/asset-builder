# Asset builder

This repository contains Dockerfile(s) to have a docker image to build assets with gulp, npm, bower, yarn ...

See docker hub image [zolweb/asset-builder](https://hub.docker.com/r/zolweb/asset-builder/)

See https://nodejs.org/en/download/ to check npm version coming with node

| Version | Docker                       | NPM   | Bower | Gulp  |
|:-------:|:----------------------------:|:-----:|:-----:|:-----:|
| 1.0     | node:8.9.3-slim (latest LTS) | 5.5.1 | 1.8.2 | 3.9.1 |

### How to use it : 

```bash
# NPM install
docker run --rm --tty \
    --volume $(PWD):/data \
    zolweb/asset-builder:1.0 \
    bash -ci "npm install"
    
# Bower install
docker run --rm --tty \
    --volume $(PWD):/data \
    zolweb/asset-builder:1.0 \
    bash -ci "bower install"
    
# Gulp usage
docker run --rm --tty \
    --volume $(PWD):/data \
    zolweb/asset-builder:1.0 \
    bash -ci "gulp"
```

There is a known issue (for example encountered [here](https://github.com/jdleesmiller/docker-chat-demo/issues/8)) with user binding for node default user created
Image assume the node user with uid 1000 is obviously the same as host
To prevent this, we have to start the container as root then change node user uid to be the same as host (each time the container is started :/)

```
# Assuming 1001 is your host UID and 1001 your host GID
# Replace "npm install" by whatever command you want to run
docker run --rm --tty \
    --volume $(PWD):/data \
    zolweb/asset-builder:1.0 \
    bash -ci "usermod -u 1001 node && groupmod -g 1001 node && sudo -i -u node && cd /data && npm install"
```

This image extends from [node docker image](https://hub.docker.com/_/node/), you can refer to it for more informations
