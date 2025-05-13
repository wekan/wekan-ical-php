# wekan-ical-php

Calendar Synchronisation for Wekan. Supports single ical files or webcal sync.

## Requirements:

* PHP (>=7)
    * `php-curl`
    * [`php-qrcode`](https://github.com/chillerlan/php-qrcode)
    * `php-mysql`

* Webserver with PHP support (e.g. Apache2)

* MySQL or MariaDB

## Install required dependencies

Ubuntu 20.04 Server (most likely also Debian 10):

```
# LAMP-stack
apt install apache2 php libapache2-mod-php mariadb-server php

# PHP modules
apt install php-curl php-mysql

# 3rdparty libraries
apt install composer
cd libs/
chmod +x ./install_all.sh
sudo -u www-data ./install_all.sh
```

## Deployment

Use the sample configuration `conf/common.php.sample` to create your
configuration file:
```
cp conf/common.php.sample conf/common.php
vi conf/common.php
```

Create a MariaDB/MySQL database with the credentials supplied in the
`common.php` config file:
```
CREATE DATABASE name_of_db;

USE name_of_db;

CREATE TABLE name_of_table (
    username CHAR(100),
    token CHAR(100),
    expire BIGINT,
    ical BIGINT)

CREATE USER name_of_user@localhost IDENTIFIED BY 'your-secure-pw';

GRANT ALL PRIVILEGES ON name_of_db.* to name_of_user@localhost;

FLUSH PRIVILEGES;
```

## Version-Upgrade

If you are running wekan-ical-php straight from `main` branch:

```
git pull
```

If you are running from a specific release:

```
git checkout main
git pull
git checkout 0.0.2
```
Either way, please take a look at the changelog from last commits or releases
and update your configurations and translations in `conf/` accordingly.
