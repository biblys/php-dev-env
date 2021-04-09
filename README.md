# Docker PHP development environement

A Docker PHP development environement used by Biblys

Enabled modules:
- mod_rewrite
- mod_expires

## Run

PHP app must have :
- a `public` directory as root
- an empty `logs` directory to store logs

From CLI:

```console
$ docker run -p 8080:80 -v '$(pwd):/usr/src/:cached' -d biblys/php-dev-env:7.2
```

Using docker-compose (example):

```yaml
version: '3.7'
services:
  biblys:
    container_name: biblys-dev-env
    image: biblys-dev-env
    build:
      context: .
      dockerfile: ./Dockerfile
    restart: on-failure
    volumes:
      - './:/usr/src/:cached'
    ports:
      - '8080:80'
```

## Update image : build & push

```console
$ git clone git@github.com:biblys/php-dev-env.git
$ cd php-7.2
$ docker build -t biblys/php-dev-env:7.2 .
$ docker push biblys/php-dev-env:7.2
```cp
