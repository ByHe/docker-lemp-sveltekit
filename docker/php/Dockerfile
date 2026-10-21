FROM php:8.5.12-fpm-alpine3.23

WORKDIR /var/www

# Alpine använder apk add istället för apt-get
RUN apk add --no-cache \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libzip-dev \
    zip \
    unzip \
    && docker-php-ext-install -j$(nproc) \
    mysqli \
    pdo_mysql \
    sockets \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip

RUN addgroup -g 1000 www \
    && adduser -u 1000 -S -s /bin/bash -G www www

COPY ./ /var/www
COPY --chown=www:www ./ /var/www

USER www