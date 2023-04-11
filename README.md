# laravel-dev-env
Docker composer for Laravel develop environment

## Getting Started
Access to docker folder and run command
```shell
docker-compose -p="laravel-dev" up --build -d
```

## Setup Laravel project
### From existing project
Copy your project to src folder
### From new project
Goto LaravelDevPhp container
```shell
docker exec -it LaravelDevPhp /bin/bash
```
Create new project
```shell
laravel new laravel
```
Move project to src folder
## Set files permission
```shell
chown -R www-data:www-data /var/www/html
```

## Config Laravel project
Database
```shell
DB_CONNECTION=mysql
DB_HOST=mariadb
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=laravel
DB_PASSWORD=123456
```
MailHog
```shell
MAIL_MAILER=smtp
MAIL_HOST=mailhog
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"
```
Redis
```shell
REDIS_HOST=redis
REDIS_PASSWORD=null
REDIS_PORT=6379
```

## Access to the container
```shell
docker exec -it LaravelDevPhp /bin/bash
docker exec -it LaravelDevNginx /bin/bash
docker exec -it LaravelDevMariadb /bin/bash
```

### References
- PHP Fpm Official https://hub.docker.com/_/php
- PHP Easy Install Extensions https://morioh.com/p/cfb07d581669
- https://github.com/thecodingmachine/docker-images-nodejs/blob/master/Dockerfile.18-bullseye
