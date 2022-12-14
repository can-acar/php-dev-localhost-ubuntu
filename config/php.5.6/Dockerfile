FROM php:5.6-fpm

# Güncel paket listelerini indir ve en güncel paketleri kur
RUN apt-get update && apt-get install -y \
    mcrypt wget zip unzip git \
    build-essential g++ \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libicu-dev \
    libzip-dev

# PHP eklentilerini yükle
RUN docker-php-ext-install iconv sockets mbstring mcrypt mysql mysqli pdo pdo_mysql \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install intl \
    && docker-php-ext-install zip

# imagick eklentisini yükle
RUN apt-get install -y libmagickwand-6.q16-dev --no-install-recommends \
    && ln -s /usr/lib/x86_64-linux-gnu/ImageMagick-6.8.9/bin-Q16/MagickWand-config /usr/bin \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && echo "extension=imagick.so" > /usr/local/etc/php/conf.d/ext-imagick.ini


RUN pecl install xdebug-2.5.5 && docker-php-ext-enable xdebug

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
RUN chmod +x /usr/bin/composer

RUN mkdir -p /app
WORKDIR "/app"

RUN usermod -u 1000 www-data && usermod -a -G users www-data