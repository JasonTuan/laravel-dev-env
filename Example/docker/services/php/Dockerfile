FROM php:8.1-fpm

WORKDIR /var/www/html

COPY local.ini /usr/local/etc/php/conf.d/local.ini

RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    git \
    jpegoptim optipng pngquant gifsicle \
    locales \
    unzip \
    vim \
    zip

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

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

# Install specific version of Node.js with npm through nvm
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
ENV NVM_DIR /usr/local/bin/nvm
RUN mkdir -p "$NVM_DIR"; \
    curl -o- "https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh" | bash \
    ; \
    source $NVM_DIR/nvm.sh; \
    nvm install --lts --latest-npm ; \
    nvm use default ;\
    node -v ; \
    npm -v ;
SHELL ["/bin/bash", "--login", "-c"]

RUN apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && chown -R www-data:www-data /var/www/html

# Install Cron
#RUN apt-get update && apt-get install -y cron
#RUN echo "* * * * * root php /var/www/artisan schedule:run >> /var/log/cron.log 2>&1" >> /etc/crontab
#RUN touch /var/log/cron.log

#CMD bash -c "cron && php-fpm"