# How to install WordPress on Ubuntu

```
apt update && apt upgrade
```

### Install Apache

```
apt install apache2
systemctl status apache2

<http://ip-address> // on Browser
```

### Install MySQL

```
apt install mysql-server mysql-client
mysql_secure_installation
```

### Install PHP

```
apt install php php-mysql
```

### Check if PHP has been installed

```
vim /var/www/html/info.php
<?php
    phpinfo();
>

<http://ip-address/info.php> // on Browser
```

### Create WordPress Database

```
mysql -u root -p
CREATE DATABASE wordpress_db;
CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL ON wordpress_db.* TO 'wp_user'@'localhost';
FLUSH PRIVILEGES;
Exit;
```

### Install WordPress CMS

```
cd /tmp && wget <https://wordpress.org/latest.tar.gz>
tar -xvf latest.tar.gz

cp -R wordpress /var/www/html/
chown -R www-data:www-data /var/www/html/wordpress/
chmod -R 755 /var/www/html/wordpress/

mkdir /var/www/html/wordpress/wp-content/uploads
chown -R www-data:www-data /var/www/html/wordpress/wp-content/uploads/
```
