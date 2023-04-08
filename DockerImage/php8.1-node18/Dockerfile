FROM php:8.1-fpm

WORKDIR /var/www/html

COPY local.ini /usr/local/etc/php/conf.d/local.ini

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    curl \
    git \
    jpegoptim optipng pngquant gifsicle \
    locales \
    unzip \
    vim \
    zip \
    nano \
    sudo \
    ca-certificates \
    procps  \
    libfontconfig  \
    tini

# Install PHP extensions

# Graphics Draw
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

# Multibyte String
RUN apt-get update && apt-get install -y libonig-dev && docker-php-ext-install mbstring

# Miscellaneous
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install exif
RUN docker-php-ext-install pdo_mysql

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer global require laravel/installer

# Install specific version of Node.js with npm through nvm
# Users in the sudoers group can sudo as root without password.
RUN useradd -ms /bin/bash docker && adduser docker sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN apt-get update &&\
    apt-get install -y --no-install-recommends gnupg &&\
    curl -sL https://deb.nodesource.com/setup_18.x | bash - &&\
    apt-get update &&\
    apt-get install -y --no-install-recommends nodejs
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - &&\
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list &&\
    apt-get update &&\
    apt-get install -y --no-install-recommends yarn
ENV PATH="$PATH:./node_modules/.bin"
RUN ln -s ~/.composer/vendor/bin/laravel /usr/local/bin/laravel
RUN chmod +x /usr/local/bin/laravel
RUN sed -i 's#/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin#/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:./node_modules/.bin:~/.composer/vendor/bin#g' /etc/sudoers

RUN apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && chown -R www-data:www-data /var/www/html

# Install Cron
#RUN apt-get update && apt-get install -y cron
#RUN echo "* * * * * root php /var/www/artisan schedule:run >> /var/log/cron.log 2>&1" >> /etc/crontab
#RUN touch /var/log/cron.log

#CMD bash -c "cron && php-fpm"