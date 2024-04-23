Docker image for Frontend developer
=====

# Included
- Node 20.12.2
- Yarn 1.22.22
- Angular Cli 17.3.5
- NX Cli
- Typescript 5.4.5
- VUE Cli 5.0.8
- Nest Js 10.3.2
- Ember 5.8.0

## Getting Started
- Example base structure for project see at github https://github.com/JasonTuan/laravel-dev-env/tree/main/Frontend

## Helpful
### Getting Started
Access to docker folder and run command
```shell
docker-compose -p="frontend-dev" up --build -d
```

### Create Frontend project
Goto FrontendDevNginx container
```shell
docker exec -it FrontendDevNginx /bin/bash
```

Create new Angular project
```shell
ng new angular-demo --routing --no-standalone --ssr=false --style=scss
```

Run Angular Project
```shell
ng serve --host=0.0.0.0 --disable-host-check
```
Goto browser and enter address
```shell
http://localhost:4200/
```
