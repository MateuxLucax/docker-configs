FROM php:7.2-fpm-alpine

COPY ./php.ini /usr/local/etc/php/conf.d/php.ini
COPY ./error_reporting.ini /usr/local/etc/php/conf.d/error_reporting.ini
COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
COPY ./www.conf /usr/local/etc/php-fpm.d/www.conf

RUN touch /tmp/xdebug.log && chmod 777 /tmp/xdebug.log

RUN apk --no-cache add tzdata \
  && cp /usr/share/zoneinfo/Brazil/East /etc/localtime \
  && echo "Brazil/East" > /etc/timezone

RUN apk add --no-cache --virtual .phpize_deps $PHPIZE_DEPS \
  && apk add --no-cache \
  libjpeg-turbo-dev \
  libpng-dev \
  libmemcached-dev \
  postgresql-dev \
  postgresql-libs \
  icu-dev \
  libzip-dev \
  zip \
  && docker-php-ext-configure gd \
  --with-png-dir=/usr/lib/ \
  --with-jpeg-dir=/usr/lib/ \
  --with-gd \
  && docker-php-ext-configure zip \
  --with-libzip \
  && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
  && docker-php-ext-install -j$(nproc) gd \
  && pecl install memcached-3.1.3 \
  && docker-php-ext-enable memcached \
  && pecl install xdebug-3.1.0 \
  && docker-php-ext-enable xdebug \
  && docker-php-ext-install -j$(nproc) opcache \
  && docker-php-ext-install -j$(nproc) pdo \
  && docker-php-ext-install -j$(nproc) pgsql \
  && docker-php-ext-install -j$(nproc) pdo_pgsql \
  && docker-php-ext-install -j$(nproc) intl \
  && docker-php-ext-install -j$(nproc) sockets \
  && docker-php-ext-install -j$(nproc) zip \
  && apk del .phpize_deps

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

EXPOSE 9003