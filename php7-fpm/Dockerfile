FROM phpdockerio/php72-fpm

RUN apt-get upgrade

RUN apt-get update && apt-get install -y --force-yes git unzip vim wget libmcrypt-dev libreadline-dev php-pear \
        bash-completion iputils-ping build-essential git-flow \
        php7.2-bcmath php7.2-bz2 php7.2-cli php7.2-common php7.2-curl \
        php7.2-cgi php7.2-dev php7.2-fpm php7.2-gd php7.2-gmp php7.2-imap php7.2-intl \
        php7.2-json php7.2-ldap php7.2-mbstring  php7.2-mysql \
        php7.2-readline php7.2-soap \
        php7.2-tidy php7.2-zip php7.2-xdebug ssh dos2unix ssmtp

RUN apt-get clean

RUN usermod -u 1000 www-data && groupmod -g 1000 www-data        
RUN sed -i 's/short_open_tag = Off/short_open_tag = On/' /etc/php/7.2/fpm/php.ini
RUN sed -i 's/post_max_size = 8M/post_max_size = 50M/' /etc/php/7.2/fpm/php.ini
RUN sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 50M/' /etc/php/7.2/fpm/php.ini

# Install Composer
RUN curl -sS https://getcomposer.org/installer \
    | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer --version \
    && composer global require "fxp/composer-asset-plugin" "balping/artisan-bash-completion"

# SSMTP settings
COPY ./ssmtp.conf /etc/ssmtp/ssmtp.conf

COPY ./.bashrc /root/.bashrc
COPY ./.gitconfig /root/.gitconfig

RUN touch /root/.bash_history

COPY ./.ssh/id* /root/.ssh/
RUN chmod -R 600  /root/.ssh

RUN curl -LO https://deployer.org/deployer.phar
RUN mv deployer.phar /usr/local/bin/dep
RUN chmod +x /usr/local/bin/dep

WORKDIR /var/www/
