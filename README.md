# Docker compose build for symfony apps
## Requirements
[docker](https://docs.docker.com/engine/installation/) + [docker compose](https://docs.docker.com/compose/install/)
## Usage
`docker-compose up`

**Connect to the php container to run php commands**

`docker exec -t -i rincevent_php bash`

** Fix cache and logs issues **
Run these commandes in the php container (see above to connect), replace DIR with your real directories

```
setfacl -R -m u:1000:rwX DIR
setfacl -dR -m u:1000:rwX DIR
```

## Description
* A code container
  * share the current directory as web root
  * change the code container volume to change the shared directory (ie: .:/var/www/ => ./src/:/var/www/)
* A php 5.6 container
  * some basic extensions and composer are installed
  * to install more extensions, use docker-php-ext-install ([see](https://hub.docker.com/_/php/)) or docker-php-pecl-install ( = pecl install)
* Nginx
  * Current port is 81 on the host machine, change it if you like
  * Currently only a default conf and no vhost. Use path like 127.0.0.1:81/web/app_dev.php
* MariaDB
  * Login : root/root and user/user
  * data is shared in data/mysql, change it if you like
  * port is not shared with the host, to share it, add
```
expose:
    - 3306
```
* MongoDB
  * data is shared in data/mongo, change it if you like
  * port is not shared with the host, to share it, add
```
expose:
    - 27017
```
* RabbitMQ + management
  * Access with 127.0.0.1:15672, login : guest/guest
