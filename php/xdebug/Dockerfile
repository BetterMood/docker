FROM bettermood/php:latest

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

COPY ./xdebug.ini $PHP_INI_DIR/conf.d/xdebug.ini