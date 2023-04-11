### laravel9-ubuntu-help

## php

sudo apt update

sudo apt install --no-install-recommends php8.1

php -v

sudo apt-get install -y php8.1-cli php8.1-common php8.1-mysql php8.1-zip php8.1-gd php8.1-mbstring php8.1-curl php8.1-xml php8.1-bcmath

sudo apt install php8.1-fpm


## composer

sudo apt update

sudo apt install php-cli unzip

curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php

sudo php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer

composer

## mysql

sudo apt update

sudo apt install mysql-server

sudo systemctl start mysql.service

sudo mysql

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

exit

sudo mysql_secure_installation

mysql -u root -p

create database 'database_name';

## nginx

sudo apt update

sudo apt install nginx

systemctl status nginx

## nginx config for laravel 9 ubuntu 22.0, php-fpm8.1

```
server {
    listen 80;
    listen [::]:80;
    server_name ;
    root /var/www/project/public;
    
    index index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

## nginx commands

sudo systemctl stop nginx

sudo systemctl start nginx

sudo systemctl restart nginx

sudo systemctl reload nginx

sudo systemctl disable nginx
