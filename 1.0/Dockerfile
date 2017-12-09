FROM node:8.8.1-slim

# Theses args are specified inside docker-compose-common file
ARG UID
ARG GID

# Change node uid to our own uid
# Note that you MUST build this image where you use it
# Install wanted packages
RUN apt-get update && apt-get install -yyq \
    sudo \
    git \
    python python-dev python-pip python-virtualenv \
    && apt-get clean \
    && usermod -u $UID node \
    && groupmod -g $GID node \
    && find / -user 1000 -exec chown -h $UID {} \; || true \
    && find / -group 1000 -exec chgrp -h $GID {} \; || true \
    && usermod -g $GID node \
    && npm install -g npm@5.6.0 \
    && npm install -g node-gyp bower@1.8.2 gulp@3.9.1 \
    && npm cache clean -f \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /data

CMD ["bash"]