# This Dockerfile is used to build an image containing an node jenkins slave used for server

FROM node:6.9.2

MAINTAINER Biju Joseph <biju.joseph@semanticbits.com>


# add more arguments from CI to the image so that `$ env` should reveal more info
ARG CI_BUILD_ID
ARG CI_BUILD_REF
ARG CI_REGISTRY_IMAGE
ARG CI_PROJECT_NAME
ARG CI_BUILD_REF_NAME
ARG CI_BUILD_TIME
ARG NG_CLI_VERSION=latest

ENV JAVA_VERSION 8u31
ENV BUILD_VERSION b13

ENV CI_BUILD_ID=$CI_BUILD_ID CI_BUILD_REF=$CI_BUILD_REF CI_REGISTRY_IMAGE=$CI_REGISTRY_IMAGE \
    CI_PROJECT_NAME=$CI_PROJECT_NAME CI_BUILD_REF_NAME=$CI_BUILD_REF_NAME CI_BUILD_TIME=$CI_BUILD_TIME

# credits to https://github.com/emmenko/docker-nodejs-karma

RUN curl https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
    && apt-get update && apt-get install -y Xvfb google-chrome-stable \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV DISPLAY :99.0
ENV CHROME_BIN /usr/bin/google-chrome

RUN apt-get update && apt-get install -y \
    openssh-server \
    python-yaml

RUN curl -O https://bootstrap.pypa.io/get-pip.py \
    && python2.7 get-pip.py \
    && pip install awscli

RUN mkdir /opt/yarn
RUN wget https://yarnpkg.com/downloads/0.23.2/yarn-v0.23.2.tar.gz -O /tmp/yarn.tar.gz && \
	tar zvxf /tmp/yarn.tar.gz -C /opt/yarn && \
	ln -s /opt/yarn/dist/bin/yarn /usr/local/bin/yarn

RUN sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd \
    && mkdir -p /var/run/sshd

# Add user jenkins to the image
RUN adduser --quiet jenkins \
    && echo "jenkins:jenkins" | chpasswd

RUN mkdir /home/jenkins/.ssh \
    && touch /home/jenkins/.ssh/known_hosts \
    && ssh-keyscan -t rsa github.com >> /home/jenkins/.ssh/known_hosts \
    && mkdir /home/jenkins/.aws \
    && touch /home/jenkins/.aws/credentials \
    && echo "[default]" >> /home/jenkins/.aws/credentials \
    && chown -R jenkins:jenkins /home/jenkins/.aws \
    && chown -R jenkins:jenkins /home/jenkins/.ssh \
    && echo "DISPLAY=:99" >> /etc/environment


RUN mkdir -p /opt/java \
    && cd /opt/java \
    && wget -P /opt/java --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.tar.gz \
    && tar xfs /opt/java/jdk-8u131-linux-x64.tar.gz -C /opt/java/ \
    && update-alternatives --install /usr/bin/java java /opt/java/jdk1.8.0_131/bin/java 9999 \
    && update-alternatives --install /usr/bin/javac javac /opt/java/jdk1.8.0_131/bin/javac 9999


ADD xvfb.sh /etc/init.d/xvfb
ADD entrypoint.sh /entrypoint.sh

RUN chmod +x /etc/init.d/xvfb \
    && chmod +x /entrypoint.sh

#RUN npm cache clean && rm -rf ~/.npm

RUN chown -R jenkins:jenkins /usr/local/lib/node_modules

# Standard SSH port
EXPOSE 22

ENTRYPOINT ["/entrypoint.sh"]