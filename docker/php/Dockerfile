FROM php:fpm

WORKDIR /var/www/laravel

RUN apt-get update
RUN apt-get install unzip git -y

RUN pecl install xdebug && docker-php-ext-enable xdebug
COPY docker-php-ext-xdebug.ini /usr/local/etc/php/conf.d

# Install Postgre PDO
RUN apt-get install -y libpq-dev \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo pdo_pgsql pgsql
RUN docker-php-ext-install pdo pdo_mysql


RUN apt-get install -y libzip-dev \
    && docker-php-ext-install zip

# GD LIB
RUN apt-get install -y libpng-dev libjpeg62-turbo-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg --with-png
    && docker-php-ext-install gd

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php ./composer-setup.php --install-dir="/usr/local/bin" --filename="composer"
RUN rm ./composer-setup.php

# Add global vendor binaries to $PATH
RUN echo export PATH=\$PATH:`composer global config bin-dir --absolute` >> ~/.bashrc

#RUN composer global require laravel/installer

USER root
