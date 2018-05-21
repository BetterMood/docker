FROM ubuntu:16.04

RUN apt-get update && apt-get install -y apache2 curl


ENV APACHE_SERVER_NAME=webserver
ENV PHP_SERVER=php

WORKDIR /etc/apache2
RUN sed -i -e 's/#ServerRoot "\/etc\/apache2"/ServerRoot "\/etc\/apache2"/g' apache2.conf

RUN a2dissite 000-default && \
    a2enmod rewrite socache_shmcb ssl proxy proxy_fcgi

COPY ./custom.conf conf-enabled/custom.conf

EXPOSE 80
EXPOSE 443

CMD ["apachectl", "-d .", "-DFOREGROUND"]