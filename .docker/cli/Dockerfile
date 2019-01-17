FROM php:7.2-fpm

ARG DOCKER_USER=dockeruser
ARG PUID=1000
ARG PGID=1000

RUN groupadd -g $PGID $DOCKER_USER && useradd -u $PUID -g $DOCKER_USER -m $DOCKER_USER && adduser $DOCKER_USER sudo

RUN apt-get update && apt-get install -y \
libmcrypt-dev

RUN docker-php-ext-install bcmath pdo_mysql

RUN curl -s http://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer
RUN chown dockeruser:dockeruser /usr/local/bin/composer

USER $DOCKER_USER
RUN mkdir -p /home/dockeruser/.composer/cache && chown dockeruser:dockeruser /home/dockeruser/.composer/cache \
&& chmod 777 -R /home/dockeruser/.composer

RUN echo "export PATH=${PATH}:~/.composer/vendor/bin" >> ~/.bashrc

WORKDIR /var/www/

EXPOSE 8080
RUN . ~/.bashrc
CMD [ "bash" ]