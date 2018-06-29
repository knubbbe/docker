FROM php:5.6-apache

RUN apt-get update -y && apt-get install -qq -y libpng-dev curl libcurl4-openssl-dev vim

RUN apt-get install -y \
        libmcrypt-dev \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install mcrypt \
    && apt-get remove -y \
        libmcrypt-dev \
    && apt-get install -y \
        libmcrypt4 \
    && apt-get autoremove -y

RUN docker-php-ext-install pdo pdo_mysql mysql mbstring gd curl
RUN pecl install memcache


RUN a2enmod headers
RUN a2enmod rewrite
COPY ./configs/vhost.conf /etc/apache2/sites-available/dev.conf
COPY ./ssl/eckerolinjen.crt /var/www/ssl/eckerolinjen.crt
COPY ./ssl/eckerolinjen.key /var/www/ssl/eckerolinjen.key
RUN a2ensite dev
RUN a2enmod ssl
RUN service apache2 restart
