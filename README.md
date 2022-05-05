# RethinkDB Alpine (Unofficial)

Minimal [rethinkdb](https://github.com/rethinkdb/rethinkdb) docker images based on [alpine](https://hub.docker.com/_/alpine).

The output of these builds are published to [docker hub](https://hub.docker.com/repository/docker/besworks/rethinkdb) as **besworks/rethinkdb**

## Tags

- `:latest` = Bare minimum install (~36MB).
    Based on alpine:3.15 and RethinkDB 2.4.2

- `:python` = With python3 + rethinkdb library (~79MB).
   Based on [python3.10-alpine3.15](https://hub.docker.com/_/python)
   with the rethinkdb binary from `:latest`

## Usage

```
docker run -d --name=rdbtest -p 8080:8080 -p 28015:28015 -p 29015:29015 besworks/rethinkdb:latest

docker logs -f rdbtest

docker stop rdbtest
```

Building `latest` from it's Dockerfile takes some time and produces a rather large intermediary build image. It's recommended to pull this version from docker hub unless you are forking this project for research/development.