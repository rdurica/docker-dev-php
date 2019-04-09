FROM php:7.3.3-apache

RUN apt-get -y update && apt-get -y upgrade && apt-get -y install \
    curl \
    zip \
    git \
    zlib1g-dev \
    libzip-dev

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl https://nodejs.org/dist/v8.9.4/node-v8.9.4-linux-x64.tar.xz | tar xJ -C /opt && \
    ln -s /opt/node-v8.9.4-linux-x64/bin/node /usr/local/bin/node && \
    ln -s /opt/node-v8.9.4-linux-x64/bin/npm /usr/local/bin/npm

RUN docker-php-ext-install \
        pdo \
        pdo_mysql \
        json \
	zip
RUN apt-get -y clean
RUN apt-get -y autoclean
RUN apt-get -y autoremove

RUN a2enmod rewrite
COPY ./vhost.conf /etc/apache2/sites-available/000-default.conf

WORKDIR /var/www/html
