---
Categories:
  - Webwork
  - Tutorial
Tags:
  - Invoice
  - Nginx
  - Arch Linux
  - Invoiceninja
Draft: false
date: 2016-05-22T12:16:00
description: Um die Anzahl der Artikelaufrufe in WordPress zu erhalten benötigt es kein Plugin. Mit einigen Zeilen Code kannst du dir ein Plugin getrost sparen.
title: Install Invoiceninja Archlinux with Nginx
---

In this tutorial i’ll see how to install Invoice Ninja on a Arch Linux VPS with MariaDB, PHP-FPM and Nginx. Invoice Ninja is a free, open-source solution for invoicing and billing customers and it’s based on Laravel framework.


Installing Required Software
----------------------------

First you must Login to your System via SSH:

    ssh user@myVPS

Requirements:

* nginx
* php-fpm
* php-mcrypt
* php-gd
* php-composer
* git
* curl
* openssl
* mariadb

First update the system:

    pacman -Syu


Setup MariaDB
-------------

Installing MariaDB ([More Information on Archlinux.org](https://wiki.archlinux.org/index.php/MySQL#Installation)
):

    pacman -S mariadb


When the installation is complete, run the following command to secure your installation:

    mysql_secure_installation

Next, we need to create a database for our Invoice Ninja instance.

```bash
    mysql -u root -p
    MariaDB [(none)]> CREATE DATABASE ininja;
    MariaDB [(none)]> GRANT ALL PRIVILEGES ON ininja.* TO 'ininjauser'@'localhost' IDENTIFIED BY 'ininjauser_passwd';
    MariaDB [(none)]> FLUSH PRIVILEGES;
    MariaDB [(none)]> \q
```

Install and configure PHP and Nginx
-----------------------------------

You should install Nginx, PHP and all necessary extensions:

    pacman -S nginx php php-mcrypt php-gd php-composer

Uncomment the following Modules for PHP `vim /etc/php/php.ini`:


    extension=curl.so
    extension=gd.so
    extension=gmp.so
    extension=iconv.so
    extension=mcrypt.so
    extension=pdo_mysql.so
    extension=zip.so


### Setup Nginx
Generate SSL certificate:

```bash
mkdir -p /etc/nginx/ssl
cd /etc/nginx/ssl
openssl genrsa -des3 -passout pass:x -out ininja.pass.key 2048
openssl rsa -passin pass:x -in ininja.pass.key -out ininja.key
rm ininja.pass.key
openssl req -new -key ininja.key -out ininja.csr
openssl x509 -req -days 365 -in ininja.csr -signkey ininja.key -out ininja.crt
```

Create a new Nginx Serverblock `vim /etc/nginx/sites-availeble/invoiceninja`:

```Nginx
server {
    listen  80;
    listen  [::]:80 ipv6only=on;
    server_name my_invoiceninja.domain.tld;

    # Return all requests to https
    return  https://$host$request_uri;
}
server {
    listen  443;
    listen  [::]:443 ipv6only=on;
    server_name my_invoiceninja.domain.tld;

    ssl on;
    ssl_certificate     /etc/nginx/ssl/ininja.crt;
    ssl_certificate_key /etc/nginx/ssl/ininja.key;
    ssl_session_timeout 5m;

    ssl_ciphers                 'AES128+EECDH:AES128+EDH:!aNULL';
    ssl_protocols               TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers   on;

    charset utf-8;

    root /srv/http/your_ninja_site/public;
    index index.php index.html index.htm;

    ## Invoiceninja Settings
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    access_log  /var/log/nginx/ininja.access.log;
    error_log   /var/log/nginx/ininja.error.log;

    sendfile off;

    location ~ /\.ht {
        deny all;
    }

    ## FastCGI Setting
    location ~ \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        if (!-f $document_root$fastcgi_script_name) {
            return 404;
        }
        # NOTE: You should have "cgi.fix_pathinfo = 0;" in php.ini

        fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
        fastcgi_read_timeout 30m;
        fastcgi_param PATH_INFO $fastcgi_path_info;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_index index.php;
        include /etc/nginx/fastcgi_params;
    }
}
```


Activate the server block by creating a symbolic link:

```bash
ln -s /etc/nginx/sites-available/your_ininja_site /etc/nginx/sites-enabled/your_ininja_site
```

### Enable PHP and Nginx

    systemctl start php-fpm
    systemctl start nginx


Install Invoice Ninja
---------------------

Create a root directory for your application.

```bash
mkdir -p /srv/http/your_ninja_site
```

Clone the project repository from GitHub:

```bash
git clone https://github.com/hillelcoren/invoice-ninja.git /srv/http/your_ininja_site
cd  /srv/http/your_ininja_site
```

Install all dependencies:

    composer install

Set the environment to production:

    cp .env.example .env

Open the database.php file and edit the database settings `vim config/database.php`:

```mysql
'mysql' => [
        'driver'    => 'mysql',
        'host'      => 'localhost',
        'database'  => 'ininja',
        'username'  => 'ininjauser',
        'password'  => 'ininjauser_passwd',
        'charset'   => 'utf8',
        'collation' => 'utf8_unicode_ci',
        'prefix'    => '',
        ],
```

Run database migrations and seed the database with sample data:

    php artisan migrate
    php artisan db:seed

Generate a new application key:

    php artisan key:generate

Insert the generated key in the configfile `vim config/app.php`:

    'key' => env('APP_KEY', '2DAdHIDKts85n6hTX82mb4GrQpX2TXZ2'),
