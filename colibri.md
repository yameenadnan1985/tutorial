To follow steps i assume you already have installed/configured docker
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

**After container start from image**
```
$ apt install php7.0
$ echo "127.0.0.1 db" >> /etc/hosts
$ service apache2 restart
```
**Create colibri user in mysql and assign permissions**
```
$ mysql
mysql > CREATE USER 'colibri'@'%' IDENTIFIED BY 'colibri';
mysql > GRANT ALL PRIVILEGES ON *.* TO 'colibri'@'%';
mysql > exit;
````

**Import ads_master and ads_school**
```
cd /var/www/html/
$ mysqladmin create ads_master;
$ mysqladmin create ads_school;
$ mysql ads_master < ads_master;
$ mysql ads_school < ads_school;
````
