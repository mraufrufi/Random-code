## MySQL  root password reset
Stop MySQL Server

'systemctl stop mysqld'

systemctl stop mysqld
Set the MySQL MYSQLD_OPTS environment to start MySQL with –skip-grant-tables

systemctl set-environment MYSQLD_OPTS="--skip-grant-tables"

systemctl set-environment MYSQLD_OPTS="--skip-grant-tables"
Start MySQL with –skip-grant-tables

systemctl start mysqld

systemctl start mysqld
Login as user root

mysql -u root

mysql -u root
Update MySQL root password

ALTER USER 'root'@'localhost' IDENTIFIED BY 'NEW_MYSQL_PASSWORD_HERE';

ALTER USER 'root'@'localhost' IDENTIFIED BY 'NEW_MYSQL_PASSWORD_HERE';
Or

UPDATE mysql.user SET authentication_string = PASSWORD('NEW_MYSQL_PASSWORD_HERE') WHERE User = 'root' AND Host = 'localhost';
FLUSH PRIVILEGES;

UPDATE mysql.user SET authentication_string = PASSWORD('NEW_MYSQL_PASSWORD_HERE') WHERE User = 'root' AND Host = 'localhost';
FLUSH PRIVILEGES;
Exit MySQL command prompt

quit

quit
