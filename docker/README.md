# Docker
> https://philipzheng.gitbook.io/docker_practice/


```
list containers
$ sudo docker container ls

enter container
$ sudo docker exec -it containerId bash


```


## docker-compose
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
