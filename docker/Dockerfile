FROM php:7.0-fpm

# Install dependencies
RUN apt-get update && apt-get install -y \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    build-essential \
    libfontconfig1 \
    libxrender1 \
    libpng-dev \
    libzip-dev \
    libicu-dev \
    libpq-dev \
    openssl \
    locales \
    unzip \
    curl \
    zip \
    vim \
    git

# Install system dependencies
RUN pecl install xdebug-2.5.5 \
    && docker-php-ext-enable xdebug

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extension GD
RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/
RUN docker-php-ext-install gd

# Install PHP extensions
RUN docker-php-ext-install pdo pdo_mysql mysqli zip exif pcntl intl bcmath

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