FROM php:8.5.12-fpm

WORKDIR /var/www

RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y \
    g++ \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libzip-dev \
    wget \
    unzip \
    zlib1g-dev \
    && docker-php-ext-install -j$(nproc) \
    mysqli \
    pdo_mysql \
    sockets \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip \
    && docker-php-source delete \
    && apt-get remove -y g++ wget \
    && apt-get autoremove --purge -y && apt-get autoclean -y && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/* /var/tmp/*

ARG UID=1000
ARG GID=1000

# Ändrat tillbaka till Debians kommandon
RUN groupadd -g ${GID} www \
 && useradd -u ${UID} -ms /bin/bash -g www www

COPY --chown=www:www . /var/www

USER www