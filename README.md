# AWS-RDS-Demo
## Migration of Database from ec2 instance to RDS instance


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

Begin Configurations for Mariadb:
```
sudo su -
apt -y install mariadb-server wget
systemctl enable mariadb
systemctl start mariadb
apt -y update
```

Set Environmental Variables:
```
DBName=demodb
DBPassword=demo12345
DBRootPassword=demo12345
DBUser=demodbuser
```

Database Setup on EC2 Instance:
```
echo "CREATE DATABASE ${DBName};" >> /tmp/db.setup
echo "CREATE USER '${DBUser}' IDENTIFIED BY '${DBPassword}';" >> /tmp/db.setup
echo "GRANT ALL PRIVILEGES ON *.* TO '${DBUser}'@'%';" >> /tmp/db.setup
echo "FLUSH PRIVILEGES;" >> /tmp/db.setup
mysqladmin -u root password "${DBRootPassword}"
mysql -u root --password="${DBRootPassword}" < /tmp/db.setup
rm /tmp/db.setup
```

Adding some dummy data to the Database inside EC2 Instance:
```
mysql -u root --password="${DBRootPassword}"
USE demodb;
CREATE TABLE table1 (id INT, name VARCHAR(45));
INSERT INTO table1 VALUES(1, 'Virat'), (2, 'Sachin'), (3, 'Dhoni'), (4, 'ABD');
SELECT * FROM table1;
```

Migration of Database in EC2 Instance to RDS Database:
```
mysqldump -u root -p ec2db > ec2db.sql
mysql -h <replace-rds-end-point-here> -P 3306 -u rdsuser -p rdsdb < ec2db.sql
mysql -h <replace-rds-end-point-here> -P 3306 -u rdsuser -p
USE rdsdb
SELECT * FROM table1;
```
