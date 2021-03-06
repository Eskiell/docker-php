# Generated via generate.sh. Please don't edit directly

FROM php:7.4-fpm-buster

ENV RUN_DEPS \
    zlib1g \
    libzip4 \
    libpng16-16 \
    libjpeg62-turbo \
    libpq5

ENV BUILD_DEPS \
    zlib1g-dev \
    libzip-dev \
    libpng-dev \
    libjpeg-dev \
    libpq-dev

ENV PHP_EXTENSIONS \
    opcache \
    zip \
    gd \
    bcmath \
    mysqli \
    pdo_mysql \
    pgsql \
    pdo_pgsql

ENV PECL_EXTENSIONS \
    redis

RUN apt-get update \
    && apt-get install -y $RUN_DEPS $BUILD_DEPS \
    && docker-php-ext-configure gd --with-jpeg \
    && docker-php-ext-install -j "$(nproc)" $PHP_EXTENSIONS \
    && apt-get purge -y --autoremove $BUILD_DEPS \
    && rm -rf /var/lib/apt/lists/*

RUN pecl install $PECL_EXTENSIONS \
    && docker-php-ext-enable $PECL_EXTENSIONS

RUN apt-get update \
    && apt-get install -y fcgiwrap \
    && rm -rf /var/lib/apt/lists/*

COPY config /usr/local/etc/php/conf.d
COPY php-fpm /usr/local/etc/php-fpm.d

COPY php-fpm-entrypoint php-fpm-healthcheck /usr/local/bin/

ENTRYPOINT [ "php-fpm-entrypoint" ]

CMD ["php-fpm"]
