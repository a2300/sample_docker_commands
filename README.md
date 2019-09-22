# DOCKER COMMANDS

### Build an image from a Dockerfile
```
docker build -t spring-boot-app:latest .
```

### Run a command in a new container
```
docker run -d -p 8080:8080 -p 5005:5005 -e "JAVA_TOOL_OPTIONS=\"-agentlib:jdwp=transport=dt_socket,address=5005,server=y,suspend=n\""  spring-boot-app:latest
```

### List containers
```
docker container ps
```

### Fetch the logs of a container
```
docker container logs <container_name>
```

### List images
```
docker image ls
```

### Stop one or more running containers
```
docker stop <container_name>
```

### Remove one or more containers
```
docker rm -f <container_name>
```

### Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
```
docker tag springio/spring-boot-app-2:latest springio/spring-boot-app-2:nonstable
```

### Run a command in a running container
(Here run command bash inside container bind-test)
```
docker exec -it bind-test bash
```


### Run a command in a new container with bounding directory to it in detach mode
(Here run a new container bind-test with directory on local c:\docker_images_test\1 bounded to /var/www/project in container from image web-test)
```

docker run --name bind-test -v c:\docker_images_test\1:/var/www/project -d web-test
```

### Create a volume and bound it to a container
```
docker volume create test-vol
docker run --name vol-test -v test-vol:/var/www/test-vol -d web-test
docker exec -it  vol-test bash
```


### Pull an image from registry
```
docker pull howtocodewell/manning-webserver-01:1.6
docker pull howtocodewell/manning-database-server-01:1.0

docker run --name mysql -e MYSQL_ROOT_PASSWORD=test -d howtocodewell/manning-database-server-01:1.0
docker run --name apache2 --link mysql -p 80:80 -d howtocodewell/manning-webserver-01:1.6
docker ps -a
```

```
docker volume create mysql_data
docker run --name mysql -v mysql_data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=test -d howtocodewell/manning-database-server-01:1.0
```

### Copy files/folders between a container and the local filesystem
```
docker run --name apache2 --link mysql -p 80:80 -d howtocodewell/manning-webserver-01:1.6 
docker cp items\file-from-host.txt apache2:/var/www/mysite-dev
docker exec -it apache2 bash
docker cp apache2:/var/www/mysite-dev/file-form-container.txt items\
```

###Mound volume from one container to another
```
docker volume create apache2_logs
docker run --name apache2 --link mysql -p 80:80 -v apache2_logs:/var/log/apache2 -d howtocodewell/manning-webserver-01:1.6 
docker run -it --name log_checker --volumes-from apache2 ubuntu
```


## Docker Compose
 
### Start the containers

  ````$ docker-compose up -d````
  
### Tear down the containers
 
  ````$ docker-compose down````
  
### Build the images
 
  ```$ docker-compose build```
