# Docker
> https://docs.docker.com/get-started/
> https://philipzheng.gitbook.io/docker_practice/


```
list containers
$ sudo docker container ls

enter container
$ sudo docker exec -it containerId bash
```


## docker hub token
> https://docs.docker.com/go/access-tokens/

## build image
```
# In Dockerfile
FROM node:12-alpine
# Adding build tools to make yarn install work on Apple silicon / arm64 machines
RUN apk add --no-cache python2 g++ make
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
```
```
$ docker build -t getting-started .
$ docker run -dp 3000:3000 getting-started
```
### update image
```
$ docker build -t getting-started . // just build again….
```


## replace container
```
$ docker ps // list containers
$ docker stop <the-container-id> // docker stop 73b58a640a5b
$ docker rm  <the-container-id> //  docker rm 73b58a640a5b
Or
$ docker rm -f <the-container-id> // it will force stop and rm
```


## push image to docker hub
```
$ docker image ls
$ docker login -u YOUR-USER-NAME
$ docker tag getting-started YOUR-USER-NAME/getting-started
$ docker push YOUR-USER-NAME/getting-started
```

## docker run with command
```
$ docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"

# docker exec command at container
$ docker exec <container-id> cat /data.txt
```
## Container Volumes
```
$ docker volume create todo-db
$ docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started
```

## Bind Mounts
```
$ docker run -dp 3000:3000 \
    -w /app -v "$(pwd):/app" \
    node:12-alpine \
    sh -c "yarn install && yarn run dev"
```

## watch log
```
$ docker logs -f <container-id>
```

## docker Network
```
$ docker run -d \
    --network todo-app --network-alias mysql \
    -v todo-mysql-data:/var/lib/mysql \
    -e MYSQL_ROOT_PASSWORD=secret \
    -e MYSQL_DATABASE=todos \
    mysql:5.7

$ docker exec -it <mysql-container-id> mysql -p // go to mysql console

$ docker run -it --network todo-app nicolaka/netshoot // another container app
$ dig mysql // using dig to find the mysql server ip at the todo-app

$ docker run -dp 3000:3000 \
  -w /app -v "$(pwd):/app" \
  --network todo-app \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=secret \
  -e MYSQL_DB=todos \
  node:12-alpine \
  sh -c "yarn install && yarn run dev"

Using docker logs to check the app connect the mysql
……
```

## Docker-Compose
it is a tool.
```
$ docker-compose version // checking exist and tool version
// write compose file
$ docker-compose up -d
$ docker-compose down
$ docker-compose up
$ docker-compose down --volumes // it will remove volumes
```
## Image Building Best
```
$ docker image history getting-started // to view history of the image
```

## docker-compose cases
### Running a new instance
```
$ sudo docker-compose -f docker.ymal -p projectName up -d
```

### Stop environment
$ sudo docker-compose -f docker.ymal -p projectName stop

### Restart stopped containers
$ sudo docker-compose -f docker.ymal -p projectName start

### Remove containers
$ sudo docker-compose -f docker.ymal -p projectName rm -v

### Remove containers and all associated images
$ sudo docker-compose -f docker.ymal -p projectName down -v

```
"docker-compose down": stop and remove the container with all the networks (but not volumes), you should add -v option to do that.
"docker-compose rm": remove stopped only containers, but not running containers, you should add option -s to be able to remove running containers
```





