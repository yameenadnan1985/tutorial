**Command to find a file with specific name**
```
find /etc -name file1.txt
```

**Command to change time zone of Server**
```
sudo timedatectl set-timezone America/New_York
```
**Command to find a file containing specific text**
```
grep -r "text-to-find-here" /
```
**Linux Command to Check Apache Access Logs**
```
tail -f /var/log/apache2/access.log
```
**Create blank empty file**
```
touch test.txt
```
**See large file with scrolling. Enter or space keys could be use**
```
cat /boot/grub/grub.cfg | less
```
**To Get Help**
```
man <command>
```
***tar command to zip/unzip**
```
tar -cvf html.tar html
tar -xvf html.tar
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
**Check version**
```
cat /etc/os-release
lsb_release -a
hostnamectl
```
**Add command output to a file**
```
# This command will append to file
echo "This is Adnan" >> test.txt

# This command will remove all previous data and will insert new data in file
echo "This is Adnan" > test.txt
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
