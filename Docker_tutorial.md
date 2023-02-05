**What is Docker**
```
Docker is open platform for developers to build, ship and run containerized applications. 
```

**Container**
```
container = object of class
# To check all running containers
$ docker ps 

# To Check all running and stop containers do this
$ docker ps -a
or
$ docker container ls -a
or 
$ docker containers -a
```

**To Check all images use this command**
```
image = template or class
$ docker images
or 
$ docker image ls
```

**Create image from Dockerfile**
```
# Go to directory where docker file is located and run this command
$ docker build -t ImageName .
# Please note dot "'" at the end of above command. This indicates that Dockerfile exists in current directory. This will build an image from Dockerfile. If you want to run docker image frist list image by using this command
$ docker images
# Take the ID of image you want to run and use this command
# Syntax is 
$ docker run image-ID e.g
$ docker run 35fg435dhdh3563

# TO RUN DOCKER CONTAINER ALL TIMES DO THIS
$ docker run -i -t image_name bash
```

**TO RUN DOCKER CONTAINER ALL TIMES DO THIS**
```
$ docker run -i -t image_name bash
$ docker run -it -p 80:80 yameen671/colibri
```

**DELETE DOCKER image(s)/container(s)**
```
# Image
$ docker rmi <your-image-id> <your-image-id>
# Remove all images at once
$ docker rmi $(docker images -q)


# Container
$ docker rm <your-container-id>
# Stop all containers
$ docker stop $(docker ps -a -q)
# Remove all stopped containers
$ docker rm $(docker ps -a -q)
```


**Docker pull/push on/from [hub.docker.com](https://hub.docker.com/)**
```
Login docker. It will ask for password, provide password
$ docker login --username=yameen671

#Push image/repository to docker hub
$ docker tag LocalRepository:LocalTag username/RemoteRepository:RemoteTag
$ docker push LocalRepository:LocalTag
$ docker tag colibri:latest yameen671/colibri:latest

#Pull image/repository from docker hub
docker pull yameen671/colibri:latest
```


**Start docker containers and get inside container**
```
$ docker ps -a
$ docker start Container-ID
$ docker exec -it <container name> /bin/bash
# Example: 
$ docker start a2e445d73f3c
$ docker exec -it agitated_spence /bin/bash
```

**Run docker with HOST files**
```
docker run -it -p 80:80 --rm -v C:\xampp\htdocs\colibri:/var/ yameen671/colibri /bin/bash
```

**Copy data between host and container**
```
 $ docker container cp CONTAINER:SRC_PATH DEST_PATH|-
 $ docker cp host container:destination
```


**To pull image and run container do this**
```
$ docker run ubuntu:20.04
```

**Binding Host Machine to Container**
```
# Here first parameter is the port of host and 2nd parameter is the port of container mmysql-server is the name of image
$ docker run -p3307:3306 mysql-server
```

**Trouble shoot why some docker command not running**
```
$ docker logs container-ID
```
