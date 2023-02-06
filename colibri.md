**Pull image and start docker from image**
```
$ docker login 
Username: yameen671
Password: D3nyAccess355@@
$ docker pull yameen671/colibri
# Once pulled create container from docker image
$ docker run -it -p 80:80 --name colibri -v C:\xampp\htdocs\colibri:/var/www/html yameen671/colibri /bin/bash
```

**Start and run container (If container already exists)**
```
$ docker start 8794c8a8a5d7
$ docker exec -it -p 80:80 8794c8a8a5d7 /bin/bash
```

**After container start **
```
# Install php
$ apt install php7.0
$ docker exec -it -p 80:80 8794c8a8a5d7 /bin/bash
```
