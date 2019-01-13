FROM php:7.2-fpm

ARG DOCKER_USER=bloodbank
ARG PUID=1000
ARG PGID=1000

RUN groupadd -g $PGID $DOCKER_USER && useradd -u $PUID -g $DOCKER_USER -m $DOCKER_USER && adduser $DOCKER_USER sudo

RUN apt-get update && apt-get install -y \
libmcrypt-dev

RUN docker-php-ext-install bcmath pdo_mysql

RUN curl -s http://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer
RUN chown bloodbank:bloodbank /usr/local/bin/composer

USER $DOCKER_USER
RUN mkdir -p /home/bloodbank/.composer/cache && chown bloodbank:bloodbank /home/bloodbank/.composer/cache \
&& chmod 777 -R /home/bloodbank/.composer

RUN echo "export PATH=${PATH}:~/.composer/vendor/bin" >> ~/.bashrc

WORKDIR /var/www/

EXPOSE 8080
RUN . ~/.bashrc
CMD [ "bash" ]