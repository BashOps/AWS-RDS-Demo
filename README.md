# AWS-RDS-Demo



Begin Configurations:
```
sudo su -
apt -y install mariadb-server wget
systemctl enable mariadb
systemctl start mariadb
apt -y update
```

PostgreSQL on EC2:
```
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql.service
sudo systemctl status postgresql.service

sudo -i -u postgres
psql
SHOW DATABASES;
CREATE DATABASE department;

CREATE TABLE employees(
id INT,
first_name VARCHAR(50),
second_name VARCHAR(30),
date_of_birth DATE,
salary INT);

\d employees
SELECT * FROM employees;

INSERT INTO employees(id, first_name, second_name, date_of_birth, salary)
VALUES(1, 'John', 'son', DATE '2024/10/3', 1000);
```

Set Environmental Variables:
```
DBName=demodb
DBPassword=demo12345
DBRootPassword=demo12345
DBUser=demodbuser
```
