Docker image for Laravel developer
=====

# Included
- PHP 8.3.3
- Node 21.6.2
- Git 2.39.2
- Laravel Installer 5.5.2
- Composer 2.7.1
- Yarn 1.22.19

## Getting Started
- Example base structure for project see at github https://github.com/JasonTuan/laravel-dev-env/tree/main/Example

## Helpful
### Getting Started
Access to docker folder and run command
```shell
docker-compose -p="laravel-dev" up --build -d
```

### Setup Laravel project
#### From existing project
Copy your project to src folder
#### From new project
Goto LaravelDevPhp container
```shell
docker exec -it LaravelDevPhp /bin/bash
```
Create new project
```shell
laravel new laravel
```
Move project to src folder
### Set files permission
```shell
chown -R www-data:www-data /var/www/html
```

### Config Laravel project
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

### Access to the container
```shell
docker exec -it LaravelDevPhp /bin/bash
docker exec -it LaravelDevNginx /bin/bash
docker exec -it LaravelDevMariadb /bin/bash
```