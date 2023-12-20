Visit link below and copy key save as signature.key
https://dev.mysql.com/doc/refman/5.7/en/checking-gpg-signature.html 
sudo apt-key add signature.key
sudo sh -c 'echo "deb http://repo.mysql.com/apt/ubuntu bionic mysql-5.7" >> /etc/apt/sources.list.d/mysql.list'
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B7B3B788A8D3785C
sudo apt-get update
sudo apt-cache policy mysql-server
sudo apt install -f mysql-client=5.7* mysql-community-server=5.7* mysql-server=5.7*

CREATE USER 'holberton_user'@'localhost' IDENTIFIED BY 'projectcorrection280hbtn';

GRANT REPLICATION CLIENT ON *.* TO 'holberton_user'@'localhost';

FLUSH PRIVILEGES;

SHOW GRANTS FOR 'holberton_user'@'localhost';

Task 2:

CREATE DATABASE tyrell_corp;

CREATE TABLE nexus6 (
id INT AUTO_INCREMENT PRIMARY KEY,
name VARCHAR(255)
);

INSERT INTO nexus6 (name) VALUES ('ODIONYE');

GRANT SELECT ON tyrell_corp.nexus6 TO 'holberton_user'@'localhost';

FLUSH PRIVILEGES;



TASK 3

CREATE USER 'replica_user'@'%' IDENTIFIED BY 'projectcorrection280hbtn';

GRANT REPLICATIO SLAVE ON *.* TO 'replica_user'@'%';
GRANT SELECT ON mysql.user TO 'holberton_user'@'localhost';
FLUSH PRIVILEGES;

SHOW GRANTS FOR 'holberton_user'@'localhost';

TASK 4
vi /etc/mysql/mysql.conf.d/mysqld.cnf
log_bin = var/log/mysql/mysql-bin.log

server-id = 1

service mysql restart
service mysql status

Login to sql database

show master status;

Note down the values of  File and Position colum

File =mysql-bin.000001
Position = 154

login to web 2

vi /etc/mysql/mysql.conf.d/mysqld.cnf

server-id       = 2
relay-log       = /var/log/mysql/mysql-relay-bin.log
log_bin         = /var/log/mysql/mysql-bin.log
binlog_do_db    = tyrell_corp

service mysql restart
service mysql status

login to server 2 sql

sudo mysql -u root -p

CHANGE MASTER TO MASTER_HOST='54.85.137.170',MASTER_USER='replica_user',MASTER_PASSWORD='projectcorrection280hbtn',MASTER_LOG_FILE='mysql-bin.000001',MASTER_LOG_POS=154;

START SLAVE;

SHOW SLAVE STATUS\G;
 

sudo ufw allow 3306 on both severs
