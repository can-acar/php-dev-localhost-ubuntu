FROM php:5.6-fpm

WORKDIR /app

RUN echo 'deb http://archive.debian.org/debian/ stretch main' > /etc/apt/sources.list \
    && echo 'Acquire::Check-Valid-Until "false";' > /etc/apt/apt.conf



# Install required packages and PHP extensions
RUN apt-get update && apt-get install -y \
    autoconf \
    build-essential \
    libmcrypt-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libmagickwand-dev \
    libtool \
    libxslt1-dev \
    mysql-client \
    libcurl4-openssl-dev \
    libxml2-dev \
    libicu-dev \
    libxslt-dev \
    libzip-dev \
    libpq-dev \
    git \
    gettext \
    libmagickwand-dev \
    && pecl install imagick-3.7.0 \
    && docker-php-ext-enable imagick \
    && pecl install xdebug-2.5.5 \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-install -j$(nproc) mbstring \
    && docker-php-ext-install -j$(nproc) xsl \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-install -j$(nproc) mysqli \
    && docker-php-ext-install -j$(nproc) soap \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-configure gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install exif \
    && docker-php-ext-install gettext

# Install composer
RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/local/bin --filename=composer

# Install redis
RUN pecl install redis-2.2.8 \
    && docker-php-ext-enable redis

# Install mongodb
RUN pecl install mongodb-1.5.4 \
    && docker-php-ext-enable mongodb

RUN mkdir -p /tmp/session
RUN chmod 777 /tmp/session

RUN mkdir -p /tmp/cache
RUN chmod 777 /tmp/cache

RUN mkdir -p /tmp/logs
RUN chmod 777 /tmp/logs

RUN mkdir -p /tmp/uploads
RUN chmod 777 /tmp/uploads

# Set the user and group to run the container
RUN usermod -u 1000 www-data && usermod -a -G users www-data
