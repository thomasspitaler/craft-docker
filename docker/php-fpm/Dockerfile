FROM php:7-fpm

RUN apt-get update

RUN apt-get install -y imagemagick
RUN apt-get install -y libmagickwand-dev --no-install-recommends
RUN apt-get install -y libzip-dev
RUN apt-get install -y libpq-dev

RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN yes '' | pecl install imagick && docker-php-ext-enable imagick
RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_pgsql
RUN docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
