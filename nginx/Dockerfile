FROM debian:jessie

RUN apt-get update && apt-get install -y \
    nginx

RUN usermod -u 1000 www-data

RUN echo "upstream php-upstream { server ntsphpserver:9000; }" > /etc/nginx/conf.d/upstream.conf

ADD nginx.conf /etc/nginx/
ADD ./conf/*.conf /etc/nginx/sites-available/

#setup nginx stuff
RUN ln -s /etc/nginx/sites-available/notthatspicy.local.conf /etc/nginx/sites-enabled/notthatspicy.local.conf
#RUN ln -s /etc/nginx/sites-available/crudtest.local.conf /etc/nginx/sites-enabled/crudtest.local.conf
RUN ln -s /etc/nginx/sites-available/torrents.local.conf /etc/nginx/sites-enabled/torrents.local.conf
RUN ln -s /etc/nginx/sites-available/deploy.notthatspicy.local.conf /etc/nginx/sites-enabled/deploy.notthatspicy.local.conf

CMD ["nginx"]

EXPOSE 80
EXPOSE 443
