# Docker PHP-FPM 8.0 & Nginx 1.18 on Alpine Linux

* Built on the lightweight and secure Alpine Linux distribution
* Very small Docker image size (+/-35MB)
* Uses PHP 8 for better performance, lower CPU usage & memory footprint
* Optimized for 100 concurrent users
* Optimized to only use resources when there's traffic (by using PHP-FPM's on-demand PM)
* The servers Nginx, PHP-FPM and supervisord run under a non-privileged user (nobody) to make it more secure
* The logs of all the services are redirected to the output of the Docker container (visible with `docker logs -f <container name>`)
* Follows the KISS principle (Keep It Simple, Stupid) to make it easy to understand and adjust the image to your needs

![nginx 1.18.0](https://img.shields.io/badge/nginx-1.18-brightgreen.svg)
![php 8](https://img.shields.io/badge/php-8-brightgreen.svg)
![License MIT](https://img.shields.io/badge/license-MIT-blue.svg)

### Includes

* Composer
* WP-CLI
* GD2
* Various other extensions (like SimpleXML)
* MySQL CLI

This image is built on GitHub actions and hosted on the GitHub Docker images repo. It is also available under `khromov/alpine-nginx-php8` on [Docker Hub](https://hub.docker.com/r/khromov/alpine-nginx-php8).

### Usage

Fetch the prebuilt image in your custom images:

GitHub (preferred):

```
git clone git@github.com:WGR-SA/alpine-nginx-php8.git
```
#### Configure a little
```
cd alpine-nginx-php8
cp ./config/localhost.default.conf ./config/localhost.conf
cp ./.env.default ./.env
```

#### Start Nginx, PHP and MySQL via docker-compose

This is convenient for developing Laravel, WordPress or Drupal sites. It includes MySQL and phpMyAdmin

```
docker-compose up
```

Now you can access your site at http://localhost:8100 and the MySQL database at `db:3306`.

You can mount your own dev folder by editing the `./env` file and change the ROOT environment var; example:

```
ROOT="/Users/foo/Sites/myWebApp.com/"
```

The urls are:
* Web: http://localhost:8100
* phpMyAdmin: http://localhost:8101

#### Quick build / run

```
docker build . -t php8
docker run -p 8100:8080 -t php8
```

Go to:  
http://localhost:8100/

## Configuration
In [config/](config/) you'll find the default configuration files for Nginx, PHP and PHP-FPM.
If you want to extend or customize that you can do so by mounting a configuration file in the correct folder.

## Acknowledgements

This image was a fork of [khromov/alpine-nginx-php8](https://github.com/khromov/alpine-nginx-php8).
