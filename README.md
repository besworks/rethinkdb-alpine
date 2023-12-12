# RethinkDB Alpine (Unofficial)

Minimal rethinkdb docker images based on alpine linux.

## Versions

### :latest (~36MB)

- Based on [alpine:3.16](https://hub.docker.com/_/alpine)
- Uses rethinkdb 2.4.4 built [from source](https://github.com/rethinkdb/rethinkdb)

### :python (~79MB)

- Based on [python:3.9-alpine3.16](https://hub.docker.com/_/python)
- Includes the [rethinkdb python driver](https://rethinkdb.com/docs/install-drivers/python/)
- Uses rethinkdb binary from [besworks/rethinkdb:latest](https://hub.docker.com/r/besworks/rethinkdb)

## Build

```
docker build -t besworks/rethinkdb:latest ./latest/
```
```
docker build -t besworks/rethinkdb:python ./python/
```

## Usage

Building **:latest** from it's Dockerfile takes some time and produces a rather large intermediary build image (~3GB). It's recommended to pull this version [from docker hub](https://hub.docker.com/repository/docker/besworks/rethinkdb) unless you are forking this project for research/development.

```
docker run -p 8080:8080 -p 28015:28015 -p 29015:29015 besworks/rethinkdb:latest
```

## Using Volumes

Dockerfile :

```
FROM besworks/rethinkdb:latest
VOLUME /data
```

docker-compose.yaml :


```
version: "3.9"
services:
  db:
    build: .
    ports:
      - 8080:8080
      - 28015:28015
      - 29015:29015
    volumes:
      - ./data:/data
```
