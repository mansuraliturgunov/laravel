FROM php:8.3.21-fpm-alpine3.20

WORKDIR /app

# Laravel uchun kerakli tizim paketlari va php-extensionlar
RUN apk add --no-cache \
    bash \
    libpng-dev \
    libjpeg-turbo-dev \
    libwebp-dev \
    libxpm-dev \
    freetype-dev \
    zip \
    unzip \
    openssl-dev \
    postgresql-dev \
    autoconf \
    make \
    gcc \
    g++ \
    linux-headers \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd pdo pdo_pgsql bcmath \
    && apk del autoconf make gcc g++ linux-headers

# Composer-ni yuklab olish (buni yoqib qo'yamiz)
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Papka ruxsatlarini to'g'rilash
RUN chown -R www-data:www-data /app

USER www-data