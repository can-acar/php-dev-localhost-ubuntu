FROM php:8.0.9-fpm

RUN apt-get update && apt-get install -y

RUN apt-get update && apt-get install -y --no-install-recommends \
        acl \
        libcurl4-openssl-dev \
        procps \
        zip \
        unzip \
        wget \
        git \
        zlib1g-dev \
        libxml2-dev \
        libzip-dev \
        libonig-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev && \
    docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ && \        
    docker-php-ext-install \    
        gd \
        zip \
        intl \
        mysqli \
        pdo \
        pdo_mysql \
        xml \
        curl \
        mbstring \
        opcache

RUN pecl install xdebug \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable xdebug

# RUN pecl install xdebug && docker-php-ext-enable xdebug

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
RUN chmod +x /usr/bin/composer

WORKDIR "/app"

RUN usermod -u 1000 www-data && usermod -a -G users www-data
