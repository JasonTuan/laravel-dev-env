FROM ubuntu/nginx:latest

WORKDIR /var/www/html

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
    tini \
    software-properties-common

# Install specific version of Node.js with npm through nvm
# Users in the sudoers group can sudo as root without password.
RUN useradd -ms /bin/bash docker && adduser docker sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN apt-get update &&\
    apt-get install -y --no-install-recommends gnupg &&\
    curl -sL https://deb.nodesource.com/setup_20.x | bash - &&\
    apt-get update &&\
    apt-get install -y --no-install-recommends nodejs

ENV PATH="$PATH:./node_modules/.bin"
RUN sed -i 's#/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin#/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:./node_modules/.bin:~/.composer/vendor/bin#g' /etc/sudoers

RUN npm install --global yarn &&\
    npm add --global nx@latest &&\
    npm install -g @angular/cli &&\
    npm install -g typescript &&\
    npm install -g @vue/cli &&\
    npm install -g @nestjs/cli &&\
    npm install -g ember-cli

RUN apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && chown -R www-data:www-data /var/www/html
