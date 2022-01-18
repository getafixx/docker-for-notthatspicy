FROM tbaltrushaitis/ubuntu-nodejs

USER root

ENV TZ="Europe/Berlin"

RUN export LC_ALL=C.UTF-8
RUN DEBIAN_FRONTEND=noninteractive
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN ln -fs /usr/share/zoneinfo/Europe/Berlin /etc/localtime

RUN apt-get upgrade -y --force-yes

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
    software-properties-common \
    libmcrypt-dev libreadline-dev \ 
    bash-completion iputils-ping \
    checkinstall libssl-dev

RUN npm install -g less yarn swagger-cli

RUN apt-get install -y nodejs

RUN npm install npm@latest -g

#RUN wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
#RUN export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
#RUN "$NVM_DIR/nvm.sh" # This loads nvm
#RUN nvm --version
#RUN nvm install --lts /* --reinstall-packages-from=node

RUN npm cache clean -f
RUN npm install -g n 
RUN n stable

EXPOSE 9001
EXPOSE 3000	
EXPOSE 3001
EXPOSE 8080
USER ${SVC_USER}

COPY ./.bashrc /home/${SVC_USER}/.bashrc
COPY ./.gitconfig /home/${SVC_USER}/.gitconfig

WORKDIR /workspaces/code/
ENTRYPOINT ["node"];
