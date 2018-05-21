# Docker Images for Better mood Developement

## Apache
The Apache container is a simple apache2 installation with a fcgi handler for php files. 
The files will be send to `PHP_SERVER` (envvar, defaults to `php`) at Port 9000.

### Basic Usage: 
`docker run -p 8080:80 -e PHP_SERVER=php -v $PWD:/var/www/html bettermood/apache:latest`

### Compose Usage:
```
webserver:
    image: bettermood/apache:latest
    volumes:
      - ./:/var/www/html
    ports:
      - "80:80"
      - "443:443"
    depends_on:
      - php
    environment:
        PHP_SERVER: php
```

## PHP
Based of the Container from [moodlehq/moodle-php-apache](https://github.com/moodlehq/moodle-php-apache), all necessary Extensions are installed,
on top of the [offical](https://hub.docker.com/_/php/) php-fpm container.

## Variants
There are different Variants available:
 - [Basic](https://hub.docker.com//r/bettermood/php/)
 - [with xdebug](https://hub.docker.com//r/bettermood/php-xdebug)
 
##Basic Usage
`docker run -n php -v $PWD:/var/www/html bettermood/php:latest`

### Compose Usage:
```
webserver:
    image: bettermood/php:latest
    volumes:
      - ./:/var/www/html
```