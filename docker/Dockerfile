FROM php:5.6-apache

RUN apt-get update -y && apt-get install -qq -y libpng-dev curl libcurl4-openssl-dev vim git

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

# Mailhog
RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail


RUN a2enmod rewrite
COPY ./configs/vhost.conf /etc/apache2/sites-available/dev.conf
RUN a2ensite dev
RUN service apache2 restart
