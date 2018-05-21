FROM php:7.1-fpm

#Install build packages and libaries
ARG APTPACKAGES="gettext libcurl4-openssl-dev libpq-dev libmysqlclient-dev libldap2-dev libxslt-dev \
    libxml2-dev libicu-dev libfreetype6-dev libjpeg62-turbo-dev libmemcached-dev \
    zlib1g-dev libpng12-dev"

ARG APTLIBS="locales libaio1 libcurl3 libgss3 libicu52 libmysqlclient18 libpq5 libmemcached11 libmemcachedutil2 \
    libldap-2.4-2 libxml2 libxslt1.1 libmcrypt-dev"

RUN apt-get update \
    && apt-get install -y --no-install-recommends $APTPACKAGES $APTLIBS curl git unzip ghostscript locales apt-transport-https


# Add locale
RUN echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen \
    && echo 'en_AU.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen

# Add PHP-extensions
RUN docker-php-ext-install \
    intl \
    mysqli \
    opcache \
    pgsql \
    soap \
    xsl \
    xmlrpc \
    zip

# Install gd
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# Instal ldap
RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install -j$(nproc) ldap

# Install external Tools
RUN pecl install solr memcached redis apcu igbinary \
    && docker-php-ext-enable solr memcached redis apcu igbinary \
    && echo 'apc.enable_cli = On' >> /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini

# Keep our image size down..
RUN pecl clear-cache \
    && apt-get remove --purge -y $APTPACKAGES \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

EXPOSE 9000