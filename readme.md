# wordpress Guide
This guide will walk you through step by step How to install wordpress with mySQL and phpmyadmin databases

* _Before we start make sure you enable SSH and establish a SSH connection to go forward._ 

***
## Step 1 
* In Step 1 we will update and make directory in root folder. 

1) you need to run update command to update server 

 ```bash
$ sudo apt-get update 
```

_After that Navigate you directory to root folder.If you not sure about what's the root folder. you can check that after running the Bottom command._
 ```bash
  $ sudo /etc/apache2/sites-available/ your-domain.com.conf
   ``` 

2) After navigating to root and make new directory.

```bash 
$ cd  /root/  

$ sudo mkdir test 
```
3) By Default you might not have write permissions in new directory. so to give all the permissions run the next Command.<br>
**username = login username.**

```bash
$ sudo chown -R  username test

$ cd test
```
***
## Step 2 - Install PHP and mySQL
 Lets follow the steps and install php and mySQL
 1) install php
 ```bash
 $ sudo apt-get install php7.2
```
2) install mySQL 
```bash
  $ sudo apt-get install mysql-server
  ```
  3) After that run the bottom command it will propmt you to change your password to strong password then follow the steps. 

  ```bash
    $ sudo mysql_secure_installation
 ```
4) To verify the installation, run the following command which will print the PHP version:
```bash
    $  php -v
```
5) To check status of MySQL:
  ```bash 
     $  sudo service mysql status
```
**Make sure it shows Active running otherwise go through all the steps and check if you miss something**
***
6) run the bottom commands to install the libraby and upgrade packages. 
```bash
    $ sudo apt-get install libApache2-mod-php7.2
    $ sudo apt-get install php7.2-mysql
    $ sudo apt-get install php7.2-mbstring
```
***
## Step 3 - Download wordpress
**_Fastest way to Get wp in the server._**<br>
1) To download the wordpress file run:
```bash
$ sudo curl -O https://wordpress.org/latest.zip
```
2) so downloaded file in compressed or zipped to unzip the file need to install unzip
```bash
$ sudo apt-get install unzip
```
3) Then to Unzip the file:
```bash
$ sudo unzip latest.zip
```
4) As i said before, due default all permission are not allowed to file so set permission to file.
* type d - premissions for wp directory
* type f - premissions for wp files
```bash
$ sudo chown www-data:www-data -R *

$ find . -type d -exec chmod 755 {} 
$ find . -type f -exec chmod 644 {}
OR- 
$ sudo chmod -R 755  /root folder
```
***
## Step 4 - Create wordpress database
1) login as root in terminal 
```bash
$ sudo mysql -u root -p
```
Enter you credentials - Usename and password<br>

2) Create databse and privileges
```bash
mysql $> CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'password';

mysql $> CREATE DATABASE "Enter Database Name";

mysql $> GRANT ALL PRIVILEGES ON databasename.* TO 'wordpressuser'@'localhost';
-> IDENTIFIED BY "password";

mysql> FLUSH PRIVILEGES;

mysql> EXIT
Bye
$  
```
***
## Setting Up the WP Configuration File from wordpress folder
1) From your web-root.Open conf file to add some setting in it.
```bash
sudo nano wp-config.php
```
add these lines in mySQL section of same file 
```bash
/**The name of the database for WordPress */
define( 'DB_NAME', 'wordpress' );

/** MySQL database username */
define( 'DB_USER', 'wordpressuser' );

/** MySQL database password */
define( 'DB_PASSWORD', 'password' );

/** MySQL hostname */
define( 'DB_HOST', 'localhost' );

/** Database Charset to use in creating database tables. */
define( 'DB_CHARSET', 'utf8' );
```
***
## Last Step - Restart apache
```bash 
$ sudo service apache2 restart
```
After That command you will be able to open wordpress in your broswer and finish some steps to get new wordpress site page. 

#### Optional 
> **If you want to easily handle all your** **MySQL database Install _phpMyAdmin_.**
```bash
$ sudo apt install phpmyadmin
```
Then click on apache2 after that **No** (in conf page) and you will be able to login on phpmyadmin page through browser with same mySQL credentials.
 
