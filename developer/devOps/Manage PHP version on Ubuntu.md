1. Get the information of PHP

```
sudo apt show php
sudo apt show php -a
```

1. Install PHP

```
sudo apt install php // this will install default PHP version
```

1. Install another PHP version

```
sudo apt install python-software-properties
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
```

1. Install PHP with the version (Apache)

```
sudo apt install php7.2
```

1. Install PHP with the version (Nginx)

```
sudo apt install php7.2-fpm
```

1. Install PHP modules to be required

```
sudo apt install php7.2-cli php7.2-mysql ....
```

1. Set default PHP version on Ubuntu

```
sudo update-alternatives --set php /usr/bin/php8.0
sudo a2dismod php7.2
sudo a2enmod php8.0
sudo systemctl restart apache2
```
