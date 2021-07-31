FROM php:8.0.3-fpm

ARG USER_ID
ARG GROUP_ID

#RUN a2enmod rewrite

RUN apt-get update && apt-get install -y zlib1g-dev g++ git libicu-dev libzip-dev zip libpng-dev \
    && docker-php-ext-install gd intl opcache pdo pdo_mysql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install bcmath

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && chmod +x /usr/local/bin/composer

RUN chown -hR www-data /var/www \
    && usermod -u ${USER_ID} www-data && groupmod -g ${GROUP_ID} www-data

WORKDIR /var/www/authorithation/app

USER "${USER_ID}:${GROUP_ID}"
