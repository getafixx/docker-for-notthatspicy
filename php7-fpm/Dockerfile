FROM phpdockerio/php74-fpm

RUN apt-get upgrade

RUN apt-get update

RUN apt-get install -y \
		git unzip vim wget libmcrypt-dev libreadline-dev \
        bash-completion iputils-ping build-essential git-flow \
        ssh dos2unix ssmtp rsync

RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN apt-get install -y php7.4

RUN apt-get update

RUN apt-get install -y libxml2-dev php7.4-curl php7.4-dev php7.4-gd php7.4-mbstring \
		php7.4-zip php7.4-mysql php7.4-xml php7.4-fpm php7.4-imagick php7.2-sqlite \
		php7.4-tidy php7.4-xmlrpc php7.4-intl php7.4-json \
		php7.4-cli php7.4-common php7.4-cgi php7.4-xdebug \
    	php-pear php7.4-gmp php7.4-bcmath php-soap  
		
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data        
RUN sed -i 's/short_open_tag = Off/short_open_tag = On/' /etc/php/7.4/fpm/php.ini
RUN sed -i 's/post_max_size = 8M/post_max_size = 50M/' /etc/php/7.4/fpm/php.ini
RUN sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 50M/' /etc/php/7.4/fpm/php.ini

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

RUN apt-get update --fix-missing

RUN apt-get install -y ffmpeg
RUN apt-get update
RUN apt-get install -y \
    ocrmypdf \
    python3-pip

WORKDIR /var/www/
