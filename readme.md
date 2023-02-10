**How to create SSH key and add SSH key for SSH Authentication**

**Create SSH Key**

On the linux machine type this and hit enter.
```
$ ssh-keygen -t rsa
```
This will create two files 

**id_rsa**

**id_rsa.pub**

on default location usually **/root/.ssh/**

Once you have created SSH Key, copy text from **id_rsa.pub (which is also called public key)** and open **authorized_keys** (which is also located on **/root/.ssh/**) file (via winscp) of the server where you want to have your access and past the text there.

Once it's done you are ready for SSH access.
CI/CD Test
