FROM serversideup/php:7.4-fpm-apache

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update; \
    apt-get -yq upgrade; \
    apt-get install -y --no-install-recommends \
    apt-utils \
    unzip \
    php7.4-gd \
    php7.4-curl \
    php7.4-mbstring \
    php7.4-zip \
    php7.4-xml;

# TODO: verificar por que o docker não está instalando o pgpsql e xdebug (mas rodando apt install php7.4-pgsql ou php7.4-xdebug funciona) 
RUN apt-get install php7.4-pgsql -y;
RUN apt-get install php7.4-xdebug -y;
RUN apt-get install php7.4-memcached -y;

RUN apt-get -yq autoremove; \
    apt clean; \ 
    rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN echo "ServerName localhost" | sudo tee /etc/apache2/conf-available/servername.conf

EXPOSE 80
