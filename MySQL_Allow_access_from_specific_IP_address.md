**STEP 1**
**Configure MySQL bind address**
```
# Find file containing bind-address and set bind-address to address of Specific IP (199.27.180.192) of server
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
# To bind multiple IP addresses use
bind-address = 199.27.180.192, 199.27.180.216
# restart mysql server
service mysql restart
```

**STEP 2**
**Allow remote access through firewall for Specific IP Addresses**
```
You can also specify a specific port that the IP address is allowed to connect to 
by adding to any port followed by the port number. For example, if you want to allow 199.27.180.92 to connect to port 3306 (mysql), use this command:

sudo ufw allow from 199.27.180.192 to any port 3306
Or 
# Good old iptables command that should work on any system
sudo iptables -A INPUT -p tcp -s 199.27.180.192 --dport 3306 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
```

**STEP 3**
**MYSQL: Allow remote connections to a particular user from a specific IP**
```
# Login as root user
$ mysql
mysql> CREATE USER 'colibri'@'199.27.180.192' IDENTIFIED BY 'colibri';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'colibri'@'199.27.180.192';
mysql> FLUSH PRIVILEGES;
```



**How to install & configure firewall**
```
Assuming you are using port 3306 for your MySQL server, 
we will need to allow this through the system firewall using ufw (uncomplicated firewall)
# Install ufw
apt install ufw
```

**Setting Up Default Policies**
```
If you’re just getting started with your firewall, the first rules to define 
are your default policies. These rules handle traffic that does not explicitly 
match any other rules. By default, UFW is set to deny all incoming connections 
and allow all outgoing connections. This means anyone trying to reach your server 
would not be able to connect, while any application within the server would be able 
to reach the outside world.

Set your UFW rules back to the defaults so you can be sure that you’ll be able to follow 
along with this tutorial. To set the defaults used by UFW, use these commands:

sudo ufw default deny incoming
sudo ufw default allow outgoing
```

**Allowing SSH Connections**
```
To configure your server to allow incoming SSH connections, use this command:
sudo ufw allow ssh
or
sudo ufw allow 22
```

**Enabling UFW**
```
sudo ufw enable

You will receive a warning that says the command may disrupt existing SSH connections. 
You already set up a firewall rule that allows SSH connections, so it should be fine to continue. 
Respond to the prompt with y and hit ENTER.

# The firewall is now active. To see the rules that you have set, run this command:
sudo ufw status verbose
```

**Allowing Other Connections**
```
sudo ufw allow http
or
sudo ufw allow 80

sudo ufw allow https
or
sudo ufw allow 443
```
