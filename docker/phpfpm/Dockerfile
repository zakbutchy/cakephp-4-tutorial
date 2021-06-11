FROM php:7.4-fpm-buster

RUN apt-get update && apt-get install -y \
    curl vim git zip unzip libicu-dev
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-configure intl \
    && docker-php-ext-install intl
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer
