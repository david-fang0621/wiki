1. Create https keys using openssl

```
sudo openssl req -x509 -days 365 -newkey rsa:2048 -keyout /home/fang/localhost.key -out /home/fang/localhost.crt

```

> Note: Common Name (e.g. server FQDN or Your name) must be localhost

> Note: Passphrass must be 4 to 1024 characters

1. Create Virtualhost conf for SSL

```
sudo nano /etc/apache2/sites-available/https.conf
```

```
Listen 443
<VirtualHost *:443>
    ServerName localhost
    DocumentRoot /var/www/html
    SSLEngine on
    SSLCertificateFile "/home/fang/localhost.crt"
    SSLCertificateKeyFile "/home/fang/localhost.key"
</VirtualHost>
```

1. Enable `https.conf`

```
sudo a2ensite https.conf
```

1. Enable SSL module

```
sudo a2enmod ssl
```

1. Restart apache

```
sudo service apache2 restart
```
