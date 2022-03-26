FROM php:7.2-apache

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update; \
    apt-get -yq upgrade; \
    apt-get install -y --no-install-recommends \
    apt-utils \
    unzip \
    apt-get -yq autoremove; \
    apt-get clean; \ 
    rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN install-php-extensions gd curl mbstring memcached pgsql zip xml pdo_pgsql 

RUN pecl install xdebug-3.1.0 && docker-php-ext-enable xdebug

EXPOSE 80
