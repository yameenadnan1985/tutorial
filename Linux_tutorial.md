**Command to find a file containing specific text**
```
grep -r "text-to-find-here" /
grep -n "Test" /etc/os-release $ Will return line number
```

**Command to find a file with specific name**
```
find /etc -name file1.txt
```

**See large file with scrolling. Enter or space keys could be use**
```
cat /boot/grub/grub.cfg | less
```

***tar command to zip/unzip**
```
tar -cvf html.tar html
tar -xvf html.tar
```

**Add command output to a file**
```
# This command will append to file
echo "This is Adnan" >> test.txt

# This command will remove all previous data and will insert new data in file
echo "This is Adnan" > test.txt
```

**Check version**
```
cat /etc/os-release
lsb_release -a
hostnamectl
```

**Command to change time zone of Server**
```
sudo timedatectl set-timezone America/New_York
```
**Linux Command to Check Apache Access Logs**
```
tail -f /var/log/apache2/access.log
```
**Check Apache Access Logs of specific IP/Website**
```
tail -f /var/log/apache2/access.log | grep "129.168.0.1"
```
**Create blank empty file**
```
touch test.txt
```
**To Get Help**
```
man <command>
```
**zip command to zip/unzip**
```
zip html.zip html
unzip html.zip
```
**service**
```
service apache2 start
service apache2 stop
service apache2 status
```
**ifconfig**
```
ifconfig
```

**VIM Editor**
```
vi test.txt
# To quit editor without saving
:q!
# To quit editor with saving
:wq
# To add data in editor press i and then press enter
i
# To escape from insert mode press scape and then press :wq
Esc > :wq

# To find text
/text_to_search
# To find next text
/text_to_search
and hit enter and then press "n" or "N"

# Find and replace
:%s/old_word/new_word/gC
# In next screen if you will select "y", it will replace occurances one by one. If you will select "a" it will replace all occurances.
```
**Nano Editor**
```
nano test.txt
```
**To see file page by page**
```
less file_path
```
**Enable SSL Certificate**
```
# System restart required
ls /etc/apache2/sites-available/
000-default.conf  default-ssl.conf
a2ensite default-ssl.conf
systemctl reload apache2
```
**Display single quote ' in awk print**
```
$ mysql -ucolibri -pcolibri -hdb < tmp.txt | grep "DB_" | awk '{print "USE "$1";SELECT \047student_id\047  FROM students;"}' > output.txt
$ cat output.txt
USE DB_S16010701;SELECT 'student_id'  FROM students;
USE DB_S22120101;SELECT 'student_id'  FROM students;
USE DB_S22121301;SELECT 'student_id'  FROM students;
USE DB_S22122002;SELECT 'student_id'  FROM students;
```
