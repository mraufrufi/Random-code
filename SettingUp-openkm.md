
# Setting up Openkm on Oracle Linux
## Installation java :

Check the java version using the following command if you already have installed java: 
```
java -version
```
If no java version found, then install one using the following command:
```
yum install java-1.8.0-openjdk-devel
```

if multiple instances of java are installed kindly set java 8 as your default java version using the following command: 
```
alternatives --config java 
```
## Installing and setup Database
### installation

```
#Download MySQL 
wget https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm 
md5sum mysql57-community -release-el7-9.noarch.rpm 
sudo rpm -ivh mysql57-community-release-el7-9.noarch.rpm
sudo yum install mysql-server
sudo systemctl start mysqld
sudo systemctl status mysqld

```
### Configuration

# Get the temporary password that was generated during installation
```
sudo grep 'temporary password' /var/log/mysqld. Log
```
Secure Configration of mysql
```
sudo mysql secure installation 
#Follow the instruction on the screen recommended to use default value 
```
Make sure SE Linux is running in permissive mode, so you can change the locations of the MySQL files.
Make the setting permanent, by editing the ``"/etc/selinux/config"`` file, setting the following values: 
```
SELINUX=permissive
```
Create directories to hold data and binary logs.
```
mkdir -p /u01/data
mkdir -p /u01/log_bin
mkdir -p /u01/tmpdir
chown -R mysql:mysql /u01
chmod -R 755 /u01
```
Stop the mysqld service using following command: 
```systemctl stop mysqld```
Modifies the `/etc/my.conf` file and add the following lines under [mysql] section
```
user=mysql
log_bin=/u01/log_bin/myDB
datadir=/u01/data
tmpdir=/u01/tmpdir
```
Start the mysqld service using following command: ``systemctl start mysqld``
Login with new root password. 
```
mysql --user=root –password
```
Create database user for openkms and set the following permissions:
```
DROP DATABASE IF EXISTS okmdb;
CREATE DATABASE okmdb DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_bin;
CREATE USER openkm@localhost IDENTIFIED BY 'Anypassword';
GRANT ALL ON okmdb.* TO openkm@localhost WITH GRANT OPTION; 
```
Edit the following file: ``$TOMCAT_HOME/OpenKM.cfg`` with the following configuration:
```
hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
hibernate.hbm2ddl=create
```
Modify the following MySQL configuration file named my.cnf and under [mysqld] add following instruction: 
```
default-storage-engine = innodb
```

## Installing OpenKM & Tomcat Bundle.
Download openkms installer form: ``https://www.openkm.com/en/download.html`` 
Copy where you want to install.
create new user
```
sudo useradd openkm
```
### Installation: 

```
java -jar OKMInstaller.jar
```

Follow on screen instructions
# NOTE:
``(Database name, username, password must be the same as (2.e.xii)``
