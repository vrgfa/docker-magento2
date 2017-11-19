# docker-magento2

[![Docker Automated Build](https://img.shields.io/docker/automated/sensson/magento2.svg)](https://hub.docker.com/r/sensson/magento2/) [![Docker Build Status](https://img.shields.io/docker/build/sensson/magento2.svg)](https://hub.docker.com/r/sensson/magento2/)

A base Magento 2 image that can be used to scale in production. This can
be used in combination with MySQL and Redis. It is opiniated and includes
support for Composer, ionCube, Redis and the required PHP modules for a basic 
Magento installation.

It does not include Magento. 

# Usage

An example `Dockerfile`

```
FROM sensson/magento2
COPY src/ /var/www/html/
```

Although volumes are supported, we recommend adding your source to the
container as that is the only way to package the entire application.

# Persistent storage

The container assumes you do not store data in a folder along with the
application. Don't use Docker volumes for scale. Use CephFS, GlusterFS or
integrate with S3 or S3-compatible services such as Fuga.io.

# Configuration

## Environment variables

Environment variable  | Description                   | Default
--------------------  | -----------                   | -------
MYSQL_HOSTNAME        | MySQL hostname                | mysql
MYSQL_USERNAME        | MySQL username                | root
MYSQL_PASSWORD        | MySQL password                | secure
MYSQL_DATABASE        | MySQL database                | magento
CRYPTO_KEY            | Magento Encryption key        | Emtpy
URI                   | Uri (e.g. http://localhost)   | http://localhost
RUNTYPE               | Set to development to enable  | Empty
ADMIN_USERNAME        | Administrator username        | admin
ADMIN_PASSWORD        | Administrator password        | adm1nistrator
ADMIN_FIRSTNAME       | Administrator first name      | admin
ADMIN_LASTNAME        | Administrator last name       | admin
ADMIN_EMAIL           | Administrator email address   | admin@localhost.com
BACKEND_FRONTNAME     | The URI of the admin panel    | admin
CURRENCY              | Magento's default currency    | EUR
LANGUAGE              | Magento's default language    | en_US
TIMEZONE              | Magento's timezone            | Europe/Amsterdam

Include the port mapping in `URI` if you run your shop on a local development
environment, e.g. `http://localhost:3000/`.

## Development mode

Setting `RUNTYPE` to `development` will turn on public error reports. Anything
else will leave it off. It will also set `display_errors` to on in PHP. This is
set to off by default.