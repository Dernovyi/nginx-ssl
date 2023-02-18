FROM php:7.0-fpm

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg-dev \
    libpng-dev \
    libzip-dev \
    libicu-dev \
    libpq-dev \
    openssl \
    unzip \
    && docker-php-ext-install -j$(nproc) intl pdo_mysql gd zip

RUN pecl install xdebug-2.5.5 \
    && docker-php-ext-enable xdebug

RUN yes | pecl install   \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.idekey=PHPSTORM" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_host = host.docker.internal" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_log='/tmp/xdebug_log/xdebug.log'" >> /usr/local/etc/php/conf.d/xdebug.ini

RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

USER www