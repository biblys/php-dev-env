# Inspired from https://blog.silarhi.fr/image-docker-php-apache-parfaite/
FROM php:8.3-apache

# Install system dependencies
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
  libicu-dev git libzip-dev zip libxml2-dev

# Install PHP & extensions
RUN docker-php-ext-install -j$(nproc) opcache pdo_mysql zip bcmath soap intl
RUN pecl install apcu && docker-php-ext-enable apcu
COPY ./conf/php.ini /usr/local/etc/php/conf.d/app.ini

# Configure Biblys site
COPY ./conf/vhost.conf /etc/apache2/sites-available/000-default.conf
COPY ./conf/apache.conf /etc/apache2/conf-available/z-app.conf
RUN a2enconf z-app
RUN a2enmod rewrite
RUN a2enmod expires

# Install composer
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
