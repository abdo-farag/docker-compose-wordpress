
# WordPress with nginx, php7-fpm, sendmail,MySQL and PhpMyAdmin
Built using Oficial images:
* [Nginx](https://hub.docker.com/_/nginx/).
* [PHP](https://hub.docker.com/_/php/) altered to install `docker-php-ext-install pdo pdo_mysql mysqli sendmail` (check `/php` folder).
* [MySQL](https://hub.docker.com/_/mysql/).
* [PHPMyAdmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin/).

## Get repo on your server
* Run `git clone https://github.com/abdo-farag/docker-compose-wordpress.git`
* Run `cd docker-compose-wordpress`

## Environment variables
* Edit `.env` and set environment variables.

```bash
# APP Name
APP=appname

# Set persistent directories for 
# the database and WordPress.
PERSISTENT_APP=/opt/wordpress
PERSISTENT_DB=/opt/mysql

# mysql
MYSQL_HOST=mysql
MYSQL_ROOT_PASSWORD=pwd
MYSQL_DATABASE=db
MYSQL_USER=user
MYSQL_PASSWORD=secret
```
# Create needed directories that will act as Persistent Volume
* Run `mkdir -p /opt/logs/nginx`
* Run `mkdir -p /opt/mysql`
* Run `mkdir -p /opt/nginx/conf.d/`
* Run `mkdir -p /opt/wordpress`
* Run `cp nginx/conf.d/* /opt/nginx/conf.d/`

## Get WordPress
Download [WordPress](https://wordpress.org/download/) into the main folder. Can change name and update `PERSISTENT_APP` value.

## Generate TLS certificate Using Let's Encrypt Docker Image

* Run `docker run -it --rm -p 443:443 -p 80:80 --name letsencrypt  -v "/etc/letsencrypt:/etc/letsencrypt" -v "/var/lib/letsencrypt:/var/lib/letsencrypt" quay.io/letsencrypt/letsencrypt:latest auth`

## Run Docker
* Run `docker-compose up` (needs [Docker Compose](https://docs.docker.com/compose/) installed).

## Once running
* Go to your [http://0.0.0.0/](http://0.0.0.0/) and start configurate WordPress.
* PhpMyAdmin at [http://0.0.0.0:8080/](http://0.0.0.0:8080/).

## Requirements
* [Docker Engine](https://docs.docker.com/installation/).
* [Docker Compose](https://docs.docker.com/compose/).
* [Docker Machine](https://docs.docker.com/machine/) (Mac and Windows only).
