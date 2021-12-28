ARG PHP_VERSION=8.0
FROM phpdockerio/php:${PHP_VERSION}-fpm


RUN apt-get update

RUN apt-get install -y \
		git unzip vim wget libmcrypt-dev libreadline-dev \
        bash-completion iputils-ping build-essential git-flow \
        ssh dos2unix ssmtp rsync software-properties-common


RUN add-apt-repository ppa:ondrej/php
RUN apt-get update

RUN apt-get install -y --fix-missing php${PHP_VERSION} php${PHP_VERSION}-curl php${PHP_VERSION}-gd php${PHP_VERSION}-mbstring \
		php${PHP_VERSION}-zip php${PHP_VERSION}-mysql php${PHP_VERSION}-xml php${PHP_VERSION}-fpm php${PHP_VERSION}-imagick \
		php${PHP_VERSION}-tidy php${PHP_VERSION}-intl php${PHP_VERSION}-json \
		php${PHP_VERSION}-cli php${PHP_VERSION}-common php${PHP_VERSION}-cgi php${PHP_VERSION}-xdebug \
    	php${PHP_VERSION}-gmp php${PHP_VERSION}-bcmath ffmpeg ocrmypdf python3-pip

RUN usermod -u 1000 www-data && groupmod -g 1000 www-data        

RUN sed -i 's/short_open_tag = Off/short_open_tag = On/' /etc/php/8.0/fpm/php.ini
RUN sed -i 's/post_max_size = 8M/post_max_size = 50M/' /etc/php/8.0/fpm/php.ini
RUN sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 50M/' /etc/php/8.0/fpm/php.ini

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --2

# handy for Justin
COPY ./.bashrc /root/.bashrc
COPY ./.gitconfig /root/.gitconfig

RUN touch /root/.bash_history

#git ssh set up for pulling and pushing
COPY ./.ssh/id* /root/.ssh/
RUN chmod -R 600  /root/.ssh

# SSMTP settings
COPY ./ssmtp.conf /etc/ssmtp/ssmtp.conf

RUN curl -LO https://deployer.org/deployer.phar
RUN mv deployer.phar /usr/local/bin/dep
RUN chmod +x /usr/local/bin/dep
   
WORKDIR /var/www/
