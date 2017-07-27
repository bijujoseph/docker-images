# This Dockerfile is used to build an image containing an node jenkins slave used for server
FROM node:8.2.1

MAINTAINER Biju Joseph <biju.joseph@semanticbits.com>


# install google chrome
RUN curl https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
    && apt-get update && apt-get install -y google-chrome-stable python-yaml ssh-askpass \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN curl -O https://bootstrap.pypa.io/get-pip.py \
    && python2.7 get-pip.py \
    && pip install awscli

RUN curl -sSL https://get.docker.com/ | sh \
    && pip install docker-compose

RUN mkdir -p ~/.aws \
    && touch ~/.aws/credentials \
    && echo "[default]" >> ~/.aws/credentials

RUN mkdir -p ~/.ssh
COPY adhoc_p /tmp/adhoc_p
RUN mv /tmp/adhoc_p ~/.ssh/id_rsa \
    && chmod 600 ~/.ssh/id_rsa \
    && ssh-keyscan github.com > ~/.ssh/known_hosts \
    && echo "Host github.com" > ~/.ssh/config \
    && echo "  IdentityFile ~/.ssh/id_rsa" >> ~/.ssh/config

ENV DISPLAY :99.0
ENV CHROME_BIN /usr/bin/google-chrome



