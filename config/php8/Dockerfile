FROM php:8.1-fpm

WORKDIR "/app"

RUN apt-get update && apt-get install -y \
    autoconf \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libicu-dev \
    libxml2-dev \
    libzip-dev \
    libonig-dev \
    libssl-dev \
    libmagickwand-dev \
    libcurl4-openssl-dev \
    libxslt-dev \
    git\
    libpq-dev \
    curl \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) intl \
    && docker-php-ext-install -j$(nproc) soap \
    && docker-php-ext-install -j$(nproc) sockets \
    && docker-php-ext-install -j$(nproc) bcmath \
    && docker-php-ext-install -j$(nproc) exif \
    && docker-php-ext-install -j$(nproc) pcntl \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-install -j$(nproc) mysqli \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-install -j$(nproc) opcache

# Install redis
RUN pecl install redis-5.3.4 \
    && docker-php-ext-enable redis

# Install mongodb
RUN pecl install mongodb-1.11.0 \
    && docker-php-ext-enable mongodb


# Install composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Install xdebug
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug


# Install imagick
RUN pecl install imagick \
    && docker-php-ext-enable imagick

RUN mkdir -p /tmp/session
RUN chmod 777 /tmp/session


RUN mkdir -p /tmp/cache
RUN chmod 777 /tmp/cache

RUN mkdir -p /tmp/logs
RUN chmod 777 /tmp/logs

RUN mkdir -p /tmp/uploads
RUN chmod 777 /tmp/uploads


RUN usermod -u 1000 www-data && usermod -a -G users www-data
