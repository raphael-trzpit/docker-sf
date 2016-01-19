# Docker compose build for symfony apps
## Requirements
[docker](https://docs.docker.com/engine/installation/) + [docker compose](https://docs.docker.com/compose/install/)
## Usage
`docker-compose up`
**Connect to the php container to run php command**
`docker exec -t -i rincevent_php bash`

## Description
* A code container
  * currently share the same directory as this one
  * change the code container volume to change the shared directory (ie: .:/var/www/ => ./src/:/var/www/)
* A php 5.6 container
  * some basic extensions and composer are installed
  * to install more extensions, use docker-php-ext-install ([see](https://hub.docker.com/_/php/)) or docker-php-pecl-install ( = pecl install)
* Nginx
  * Current port is 81 on the host machine, change it if you like
  * Currently only a default conf and no vhost. Use path like 127.0.0.1:81/web/app_dev.php
* MariaDB
  * Login : root/root and user/user
  * port is not shared with the host, to share it, add
```
expose:
    - 3306
```
  * data is shared in data/mysql, change it if you like
* MongoDB
  * port is not shared with the host, to share it, add
```
expose:
    - 27017
```
  * data is shared in data/mongo, change it if you like
* RabbitMQ + management
  * Access with 127.0.0.1:15672, login : guest/guest
