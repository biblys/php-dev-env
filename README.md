# Docker PHP development environment

A Docker PHP development environment used by Biblys

Enabled modules:
- mod_rewrite
- mod_expires

## Run

PHP app must have :
- a `public` directory as root
- an empty `logs` directory to store logs

From CLI:

```console
$ docker run -p 8080:80 -v '$(pwd):/usr/src/:cached' -d biblys/php-dev-env:8.1
```

Using docker-compose (example):

```yaml
services:
  biblys:
    container_name: biblys-dev-env
    image: biblys/php-dev-env:8.1
    restart: on-failure
    volumes:
      - './:/usr/src/:cached'
    ports:
      - '8088:80'
```

## Update image : build & push

```shell
php_version=8.1
cd php-$php_version
docker build -t biblys/php-dev-env:$php_version .
docker push biblys/php-dev-env:$php_version
```
