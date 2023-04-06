FROM php:8.1-fpm

# Set working directory
WORKDIR /var/www/html

# installs basic tools, then postgres ppa then nodejs ppa then nodejs and postgresql-client packages
# (and some other required dependencies). It then installs and configures several php extensions
# including pdo_pgsql and redis. Finally, it downloads and installs composer in the image.
RUN apt-get update \
    && apt-get install -y gnupg curl wget ca-certificates unzip lsb-release \
    && curl -fsSL https://deb.nodesource.com/setup_19.x | sudo -E bash - &&\
    && apt-get install -y \
        libicu-dev \
        libpq-dev \
        libzip-dev \
        nodejs \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && npm install -g npm \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && chown -R www-data:www-data /var/www/html

WORKDIR /var/www/html
USER www-data
