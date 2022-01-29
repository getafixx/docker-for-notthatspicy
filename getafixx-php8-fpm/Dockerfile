FROM phpdockerio/php80-fpm

RUN apt-get update

RUN apt-get install -y \
    git unzip vim wget libmcrypt-dev libreadline-dev \
    bash-completion iputils-ping build-essential git-flow \
    ssh dos2unix ssmtp rsync software-properties-common

RUN add-apt-repository ppa:ondrej/php
RUN apt-get update

RUN apt-get install -y --fix-missing php8.0 php8.0-curl php8.0-gd php8.0-mbstring \
    php8.0-zip php8.0-mysql php8.0-xml php8.0-fpm php8.0-imagick \
    php8.0-tidy php8.0-intl \
    php8.0-cli php8.0-common php8.0-cgi php8.0-xdebug \
    php-pear php8.0-gmp php8.0-bcmath php-soap php8.0-sqlite3 ffmpeg ocrmypdf python3-pip    

RUN sed -i 's/short_open_tag = Off/short_open_tag = On/' /etc/php/8.0/fpm/php.ini
RUN sed -i 's/post_max_size = 8M/post_max_size = 50M/' /etc/php/8.0/fpm/php.ini
RUN sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 50M/' /etc/php/8.0/fpm/php.ini

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --2

RUN curl -LO https://deployer.org/deployer.phar
RUN mv deployer.phar /usr/local/bin/dep
RUN chmod +x /usr/local/bin/dep

WORKDIR /var/www/