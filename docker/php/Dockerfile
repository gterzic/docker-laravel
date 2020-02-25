FROM php:fpm

WORKDIR /var/www/laravel

RUN apt-get update
RUN apt-get install unzip git -y

# Install Postgre PDO
#RUN apt-get install -y libpq-dev \
#    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
#    && docker-php-ext-install pdo pdo_pgsql pgsql

RUN apt-get install -y libzip-dev \
    && docker-php-ext-install zip

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php ./composer-setup.php --install-dir="/usr/local/bin" --filename="composer"
RUN rm ./composer-setup.php

# Add global vendor binaries to $PATH
RUN echo export PATH=\$PATH:`composer global config bin-dir --absolute` >> ~/.bashrc

RUN composer global require laravel/installer

USER root
