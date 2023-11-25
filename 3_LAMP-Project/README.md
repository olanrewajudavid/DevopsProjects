# LAMP Stack Project Implementation

## In this project, we will be demonstrating the installation of LAMP Server in following steps

# 1. Installing Apache and updating Firewall

## Firstly, there is need to run the command

**`sudo apt update`** 

![Apt Update](./img/1a_sudo_apt_update.png)


Then Instal Apache using Ubuntu’s package manager ‘apt’:

**`sudo apt install apache2`**
![Apt Update](./img/1b_install_appache.png)

To verify that apache2 is running; run the command bellow

**`sudo systemctl status apache2`**

![Apache Status](./img/1_apache2-Status.png)

## Add rule to AWS EC2 configuration to open inbound connection through port 80. 

**To Verify apache2 webpage is accessible from the server; use any of the following code**

**`curl http://localhost:80  
or curl http://<public address>:80`**

This can be seen below

![Apache Status](./img/curl_view.png)


## Test your serve by copying the public address and pasting it on web browser... It works!!!

![Apache on Web browser](./img/3_check-apache-on-webbrowser.png)


# 2. INSTALLING MYSQL

Install Mysql on the ubuntu server.

 **`$ sudo apt install mysql-server -y`**

![Apache on Web browser](./img/8_install-mysql.png)

Log into the MySQL console


```Note: I have run sudo -i to gain super admin access to my linux as sudo may not appear in some of the commands in the screenshots```

**`sudo mysql`**
![OpenMySQL](./img/9_mysql-command-view.png)


Then configure a database user on and set login password for Mysql

**`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Password.1';`**




Start MYSQL Interactive script, this will prompt you to configure the validate password plugin.

**`sudo mysql_secure_installation`**
![Secure Installations](./img/13a_secure-installation.png)

![Open and exit MySQL](./img/13b_secure-installation.png)


## Confirm and Check the mysql authentication access by typing the command 

**`mysql -p`**

Then exit the shell with the command:  **`exit`**

![Open and exit MySQL](./img/14_check-mysql-access.png)

# 3. INSTALLING PHP


3 packages will be installed namely php, libapache2-mod-php, php-mysql. 

**`sudo apt install php libapache2-mod-php php-mysql`**

![Php version](./img/15_install-php.png)

Confirm the php version

**`php -v`**

![Php version](./img/5_php-version-installed.png)

At this point we have successfully installed all 4 applications that make up the lamp stack

- [x] Linux
- [x] Apache Http Server
- [x] MySQL
- [x] PHP



##  ...........CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE .........

We will setup a virtual host to test the PHP script, virtual host enables you to setup multiple websites on a single server.

Create the directory for projectlamp using ‘mkdir’ command

**`sudo mkdir /var/www/projectlamp`**

Next, assign ownership of the directory with your current system user:

**`sudo chown -R $USER:$USER /var/www/projectlamp`**

As seen in the diagram below

![Projectlamp Directory](./img/19_mkdir-file-projectlamp.png)

Create and open a new configuration file in Apache’s sites-available directory.

**`sudo vi /etc/apache2/sites-available/projectlamp.conf`**

Paste below code into the file created above.
```
<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
![Configuration file](./img/20_create-file.png)


Enable the new virtual host with the a2ensite command 

**`sudo a2ensite projectlamp`**

Disable the default site with a2dissite command

**`sudo a2dissite 000-default`**

![Enable and Disable hosts](./img/21_enable-and-disable.png)

Reload Apache service for changes to take efffect

**`sudo systemctl reload apache2`**

**Create an index file in the projectlamp folder.**

```
sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html

```

![Index File](./img/22.png)

Go to your browser and try to open your website URL using IP address:

**`http://<Public-IP-Address>:80`** 

## Great!!! It works!
![Index File](./img/23.png)

# 5. ENABLE PHP ON THE WEBSITE

Edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive:

**`sudo vim /etc/apache2/mods-enabled/dir.conf`**

```
<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```
![Php version](./img/16_edit-index-file.png)


Restart the apache using the command below.

**`sudo systemctl reload apache2`**

![Apache Restarting](./img/17_restart-apache.png)

Create a new file named index.php inside the projectlamp root folder:

**`vim /var/www/projectlamp/index.php`**

```
<?php
phpinfo();

```
![Apache Restarting](./img/24_insert-into-index-php.png)

## Refreshing the page; It looks like below

![Php_homepage](./img/25_final-page.png)

It is advisable to remove the file as it contains sensitive information about your server and php site config.

**`sudo rm /var/www/projectlamp/index.php`**

# **----------------The Job is DONE!!! Thank you!!---------------**

