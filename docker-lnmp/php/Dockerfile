FROM php:7.4-fpm
RUN apt-get update && apt-get install -y \
        zlib1g-dev libzip-dev \ 
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libmemcached-dev \
        zlib1g-dev \
        libcurl4-openssl-dev \
        libxml2-dev \
        --no-install-recommends && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install -j$(nproc) mysqli pdo_mysql zip bcmath opcache sockets \
    && docker-php-ext-configure gd  --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && pecl install mcrypt-1.0.4 redis-5.3.4 xdebug-3.0.4 swoole-4.7.1\
    && docker-php-ext-enable mcrypt redis xdebug swoole \
    && docker-php-ext-configure opcache --enable-opcache && docker-php-ext-install opcache
    # redis 扩展

    # Install Composer
    RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer


#CMD ["php-fpm", "-F"]
