FROM php:8.1-fpm

WORKDIR "/app"

RUN apt-get update && apt-get install -y \
		cron g++ gettext libicu-dev openssl \
    	libc-client-dev libkrb5-dev  \
    	libxml2-dev libfreetype6-dev \
    	libgd-dev libmcrypt-dev bzip2 \
    	libbz2-dev libtidy-dev libcurl4-openssl-dev \
    	libz-dev libmemcached-dev libxslt-dev git-core libpq-dev \
    	libzip4 libzip-dev libwebp-dev	\
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev \
	&& docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg \
	&& docker-php-ext-install -j$(nproc) gd




# PHP Configuration
RUN docker-php-ext-install bcmath bz2 calendar  dba exif gettext iconv intl  soap tidy xsl zip&&\
    docker-php-ext-install mysqli pgsql pdo pdo_mysql pdo_pgsql  &&\
    docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp &&\
    docker-php-ext-install gd &&\
    docker-php-ext-configure imap --with-kerberos --with-imap-ssl &&\
    docker-php-ext-install imap &&\
    docker-php-ext-configure hash --with-mhash &&\
    pecl install mongodb && docker-php-ext-enable mongodb &&\
    pecl install redis && docker-php-ext-enable redis && \
    curl -sS https://getcomposer.org/installer | php \
            && mv composer.phar /usr/bin/composer


RUN apt-get install --yes --force-yes libmagickwand-dev libmagickcore-dev
RUN yes '' | pecl install -f imagick &&\
    docker-php-ext-enable imagick


# Install xdebug
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug



RUN usermod -u 1000 www-data && usermod -a -G users www-data
