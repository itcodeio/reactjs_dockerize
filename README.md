# ReactJS Dockerize Boilerplate 

It uses for dockerize reactjs app, quick setup of the server enviroment and deploy an app to the server.

## Remote enviroment
### Install Docker
```
sudo apt-get update
sudo apt install docker.io
sudo apt install docker-compose
sudo chown $USER /var/run/docker.sock
```
### Login to Docker hub
docker login -u itcode -p [password]

### [Variant A] Clone GIT repository
```
mkdir /home/ubuntu/srv
cd /home/ubuntu/srv
git clone https://github.com/itcodeio/reactjs_dockerize.git .
```

### Set env param
```
cp .env.sample .env
vim .env
```
e.g.

```
REACTJS_DOCKER_REPOSITORY=itcode/[projectname]:[tagname]
```

### Run docker container via docker compose 
```
docker-compose up -d --build --force-recreate
```

### [Variant B] Run docker container directly without clonning repository
```
docker run -d -p 80:80 itcode/[projectname]:[tagname]
```

## Local enviroment
### Prepare project configuration
Review example folder and select solution: docker only or docker with pm2.
Copy files from example folder to your project folder.

```
cp example/.dockerignore ./[:poject_folder]
cp example/[:solution]/Dockerfile ./[:poject_folder]
cp -R nginx/ ./[:poject_folder]
```

### Turn off copying .env.sample to .env if there is not configuration file in yout project
comment the following line: COPY .env /app/.env
```
vim Dockerfile
```

### Change node version for old codebase (optional)
e.g. change 
```
FROM node:lts as build-stage 
```
to
```
FROM node:14 as build-stage
```

### Login to Docker hub as well
```
docker login -u itcode -p [password]
```

### Make a fresh docker image and push to docker hub repository
```
docker build . -t itcode/[projectname]:[tagname]
docker push itcode/[projectname]:[tagname]
```
