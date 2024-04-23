Docker image for Frontend Developer
=====

## Getting Started
- Example base structure for project see at github https://github.com/JasonTuan/laravel-dev-env/tree/main/Frontend

## Helpful
### Getting Started
Access to docker folder and run command
```shell
docker-compose up --build -d
```

### Create Frontend project
Goto FrontendJsDevNginx container
```shell
docker exec -it FrontendDevNginx /bin/bash
```

### Create new Angular project
```shell
ng new angular-demo --routing --no-standalone --ssr=false --style=scss
```

Run Angular Project
```shell
ng serve --host=0.0.0.0 --disable-host-check
```
Goto browser and enter address
```shell
http://localhost:4201/
```

### Create new React project
```shell
npx create-next-app@latest
```

Run Angular Project
```shell
npm run dev
```
