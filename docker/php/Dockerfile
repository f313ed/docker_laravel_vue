FROM php:8.1-fpm

# COPY php.ini
COPY ./docker/php/php.ini /usr/local/etc/php/php.ini

# Composer install
COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

# install Node.js
COPY --from=node:16.15 /usr/local/bin /usr/local/bin
COPY --from=node:16.15 /usr/local/lib /usr/local/lib

RUN apt-get update && \
    apt-cache search libpq && \
    apt-get -y install \
    git \
    zip \
    unzip \
    vim \
    libpq-dev \
    && echo "deb http://deb.debian.org/debian bullseye main" > /etc/apt/sources.list.d/bullseye.list \
    && apt-get update \
    && apt-get -y install libpq-dev \
    && docker-php-ext-install pdo_pgsql bcmath
ENV TZ=Asia/Tokyo
WORKDIR /var/www/html