1. Create an AWS account
2. Create an EC2 instance
3. Login to your EC2 instance
4. Install Nginx

```
sudo add-apt-repository ppa:nginx/stable
sudo apt-get update
sudo apt-get install nginx
nginx -v
```

1. Install php7.2

```
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get install php7.4 php7.4-mysql php7.4-fpm php7.4-xml php7.4-gd php7.4-opcache php7.4-mbstring
php -v
```

1. Install additional libraries

```
sudo apt-get install zip unzip php7.2-zip
```

1. Install Composer

```
curl -sS <https://getcomposer.org/installer> | php

cd /var/www
composer create-project laravel/laravel test — prefer-dist
chown -R www-data:www-data test/
chmod -R 775 test/
```

1. Configure VirtualHost on Nginx

```
cd /etc/nginx/sites-available
vim mytestapp.conf

server {
    listen 80 default_server;
    listen [::]:80 default_server;
    root /var/www/test/public;
    index index.php index.html index.htm index.nginx-debian.html;
    server_name _;
    location / {
        try_files $uri $uri/ =404;
    }
    location ~ \\.php$ {
        include snippets/fastcgi-php.conf;
        # With php-fpm (or other unix sockets);
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        # With php-fpm (or other unix sockets);
    }
}

> Tips: `:wq` // to write and close the vim
```

1. Create a soft link to the virtual host

```
ln -s /etc/nginx/sites-available/mytestapp.conf /etc/nginx/sites-enabled
```

1. Test nginx configuration & restart Nginx

```
nginx -t
service nginx restart
```
