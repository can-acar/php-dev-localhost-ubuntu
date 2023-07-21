FROM php:5.6.40-fpm

WORKDIR /app

RUN echo 'deb http://archive.debian.org/debian/ stretch main' > /etc/apt/sources.list \
    && echo 'Acquire::Check-Valid-Until "false";' > /etc/apt/apt.conf



RUN apt-get update && apt-get install -y libmagickwand-dev --no-install-recommends && rm -rf /var/lib/apt/lists/*



# Install required packages and PHP extensions
RUN apt-get update && apt-get install -y \
    autoconf \
    build-essential \
    libmcrypt-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
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
    &&docker-php-ext-install -j$(nproc) iconv mcrypt \
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


RUN apt-get update && apt-get install -y \
    libmagickwand-dev --no-install-recommends

RUN cd /tmp \
    && curl -O -k https://pecl.php.net/get/xdebug-2.5.5.tgz \
    && tar zxvf xdebug-2.5.5.tgz \
    && cd xdebug-2.5.5 \
    && phpize && ./configure && make && make install \
    && docker-php-ext-enable xdebug \
    && cd .. && rm -r xdebug-2.5.5.tgz


RUN cd /tmp \
    && curl -O -k https://pecl.php.net/get/imagick-3.4.4.tgz \
    && tar zxvf imagick-3.4.4.tgz \
    && cd imagick-3.4.4 \
    && phpize && ./configure && make && make install \
    && docker-php-ext-enable imagick \
    && cd .. && rm -r imagick-3.4.4

RUN cd /tmp \
    && curl -O -k https://pecl.php.net/get/redis-2.2.8.tgz \
    && tar zxvf redis-2.2.8.tgz \
    && cd redis-2.2.8 \
    && phpize && ./configure && make && make install \
    && docker-php-ext-enable redis \
    && cd .. && rm -r redis-2.2.8.tgz

RUN cd /tmp \
    && curl -O -k https://pecl.php.net/get/mongodb-1.5.4.tgz \
    && tar zxvf mongodb-1.5.4.tgz \
    && cd mongodb-1.5.4 \
    && phpize && ./configure && make && make install \
    && docker-php-ext-enable mongodb \
    && cd .. && rm -r mongodb-1.5.4.tgz


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
