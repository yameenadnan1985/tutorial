**What is Docker**
```
Docker is open platform for developers to build, ship and run containerized applications. 
```

**Container**
```
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
$ docker images
or 
$ docker image ls
```

**To stop and start docker containers do this**
```
$ docker stop Container-ID
$ docker start Container-ID
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

**TO RUN DOCKER CONTAINER ALL TIMES DO THIS**
```
$ docker run -i -t image_name bash
```
