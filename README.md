# AWS-RDS-Demo



Begin Configurations:
```
sudo su -
apt -y install mariadb-server wget
systemctl enable mariadb
systemctl start mariadb
apt -y update
```
```
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql.service
sudo systemctl status postgresql.service

sudo -i -u postgres
psql
SHOW DATABASES;
CREATE DATABASE employees;

CREATE TABLE department(
id INT
```

Set Environmental Variables:
```
DBName=demodb
DBPassword=demo12345
DBRootPassword=demo12345
DBUser=demodbuser
```
