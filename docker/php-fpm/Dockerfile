FROM php:fpm
    
RUN apt-get update && apt-get install --no-install-recommends -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng16-16 \
        libpq-dev \
        libgd3 \
        libwebp6 \
        libx11-6 \
        libxpm4 \
        ucf \
        libmemcached-dev \
        libmagickwand-dev \
        zlib1g-dev \
        libicu-dev \
        g++ \
    && rm -rf /var/lib/apt/lists/* /var/www/html

RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install pdo_pgsql \
    && pecl install memcached \
    && pecl install redis \
    && pecl install xdebug \
    && pecl install imagick \
    && pecl install apcu \
    && pecl install apcu_bc-1.0.3 \
    && docker-php-ext-enable apcu --ini-name 10-docker-php-ext-apcu.ini \
    && docker-php-ext-enable apc --ini-name 20-docker-php-ext-apc.ini \
    && docker-php-ext-enable memcached \
        redis \
        xdebug \
        imagick

    

CMD ["php-fpm"]  
EXPOSE 9000
