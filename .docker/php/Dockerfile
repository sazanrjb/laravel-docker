FROM php:7.2-fpm

RUN apt-get update && apt-get install -y libmcrypt-dev mysql-client \
    && docker-php-ext-install pdo_mysql bcmath

WORKDIR /var/www