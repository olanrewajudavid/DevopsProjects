# PROJECT 6 - IMPLEMENTING CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS)

 ## **This project demonstrates hoe to implement Client Server Architecture using MySQL Databse Management System (DBMS).**

 ## 1. Create 2 Linux-based virtual servers on AWS: 
Server A name - `mysql_server` <br> 
Server B name - `mysql_client`
 
 ![Instance Creation](./img/1a.png)
 ![Instance Creation](./img/1b.png)
 ![Instance Creation](./img/1c.png)

## 2. Install MySQl server on the first instance (mysql_server):

### Run the following commands:
```
sudo apt update
sudo apt install mysql-server
mysql --version

```
![mysql-installation](./img/2a.png)
![mysql-installation](./img/2b.png)
![mysql-installation](./img/2c.png)

### Create Database, Username, Password and grant priveledges on the user
![mysql-installation](./img/2d.png)
![mysql-installation](./img/2f.png)
![Grant Priveledges](./img/2g.png)

## 3. Install MySQl client on the first instance (mysql_client):

### Run the following commands:
```
sudo apt update
sudo apt install mysql-server
mysql --version

```
![mysql-installation](./img/2a.png)
![mysql-installation](./img/3b.png)
![mysql-installation](./img/3c.png)

## 4. Edit Inbound rule on mysql_client:
![Inbound-Rule](./img/4.png)

## 5. Configure MySQL server to allow connections from remote hosts.

`sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf`
<br><br>
![Inbound-Rule](./img/5.png)

## Finnally: Connect to mysql_server from mysql_client and show databases using the command as below:

```
mysql -u example_user -h 172.31.37.15 -p
show databases;
```

![Connect to Mysql-server](./img/7.png)
# ----------------------END of Project! Thank you-----------------------