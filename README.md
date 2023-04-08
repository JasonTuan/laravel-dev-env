# laravel-dev-env
Docker composer for Laravel develop environment

## Getting Started
Access to docker folder and run command
```shell
docker-compose up --build -d
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
DB_HOST=127.0.0.1
DB_PORT=3307
DB_DATABASE=laravel
DB_USERNAME=laravel
DB_PASSWORD=123456
```
MailHog
```shell
MAIL_MAILER=smtp
MAIL_HOST=127.0.0.1
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"
```

## Access to the container
```shell
docker exec -it LaravelDevPhp /bin/bash
docker exec -it LaravelDevNginx /bin/bash
docker exec -it LaravelDevMariadb /bin/bash
```

### References
- https://github.com/thecodingmachine/docker-images-nodejs/blob/master/Dockerfile.18-bullseye
