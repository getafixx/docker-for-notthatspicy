FROM tbaltrushaitis/ubuntu-nodejs

USER root

ENV TZ="Europe/Berlin"

RUN export LC_ALL=C.UTF-8
RUN DEBIAN_FRONTEND=noninteractive
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN ln -fs /usr/share/zoneinfo/Europe/Berlin /etc/localtime

RUN apt-get update

RUN apt-get install -y tzdata
RUN dpkg-reconfigure --frontend noninteractive tzdata
RUN apt-get install -y \
    sudo \
    wget \
    zip \
    unzip \
    curl \
    ssh \
    openssh-client \
    git \
    build-essential \
    vim \
    git-flow \
    dos2unix \
    apt-utils \
    software-properties-common 

RUN npm install -g less yarn swagger-cli

EXPOSE 9001
EXPOSE 3001
EXPOSE 3000	
EXPOSE 8080

USER ${SVC_USER}

COPY ./.bashrc /home/${SVC_USER}/.bashrc
COPY ./.gitconfig /home/${SVC_USER}/.gitconfig

WORKDIR /var/www/
ENTRYPOINT ["node"];