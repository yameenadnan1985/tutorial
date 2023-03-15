**Find file containing bind-address and set bind-address to address of Specific IP of server**
```
grep -r bind-address /etc/
Example:
/etc/mysql/mariadb.conf.d/50-server.cnf

# Edit file containing bind-address
vi /etc/mysql/mariadb.conf.d/50-server.cnf

Find the setting that says bind-address underneath the [mysqld] section. 
By default, this should currently be configured to the loopback address 127.0.0.1. 
Delete that address and put your server’s public IP address in its place. 
We will just use 199.27.180.192 for the sake of the example. 
[mysqld]
bind-address = 199.27.180.192

# restart mysql server
service mysql restart
```

**Test**
