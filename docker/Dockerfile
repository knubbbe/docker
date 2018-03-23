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


RUN a2enmod rewrite
RUN service apache2 restart
