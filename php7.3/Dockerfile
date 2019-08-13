FROM php:7.3.8-apache

#Nodejs
RUN curl https://nodejs.org/dist/v10.16.2/node-v10.16.2-linux-x64.tar.xz | tar xJ -C /opt && \
    ln -s /opt/node-v10.16.2-linux-x64/bin/node /usr/local/bin/node && \
    ln -s /opt/node-v10.16.2-linux-x64/bin/npm /usr/local/bin/npm

#Yarn
RUN curl -o- -L https://yarnpkg.com/install.sh | bash && export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH"

#Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apt-get -y update && apt-get -y upgrade && apt-get -y install \
    curl \
    zip \
    git \
    zlib1g-dev \
    libzip-dev

#PHP Extensions
RUN docker-php-ext-install \
        pdo \
        pdo_mysql \
        json \
	    zip \
	    opcache

#XDebug
RUN pecl install xdebug && docker-php-ext-enable xdebug

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

RUN a2enmod rewrite

RUN apt-get -y clean && apt-get -y autoclean && apt-get -y autoremove

RUN echo "zend_extension=xdebug.so" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_handler=dbgp" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_autostart=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_connect_back=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.idekey=PHPSTORM" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_host=172.17.0.1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

WORKDIR /var/www/html