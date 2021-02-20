FROM ubuntu

USER root

ENV TZ="Europe/Berlin"

RUN export LC_ALL=C.UTF-8
RUN DEBIAN_FRONTEND=noninteractive
#RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN ln -fs /usr/share/zoneinfo/Europe/Berlin /etc/localtime

RUN apt-get upgrade -y 

RUN apt-get update -y

RUN apt-get -y install \    
    ca-certificates software-properties-common curl \
    unzip git unzip vim wget libmcrypt-dev libreadline-dev \
    bash-completion iputils-ping build-essential git-flow \
    ssh dos2unix rsync ocrmypdf

#RUN locale-gen en_US.UTF-8
#ENV LANG en_US.UTF-8
#ENV LANGUAGE en_US:en
#ENV LC_ALL en_US.UTF-8

# no more lines below this one
COPY ./.bashrc /root/.bashrc

WORKDIR /var/www/ocr
