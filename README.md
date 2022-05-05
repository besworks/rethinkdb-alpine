# RethinkDB Alpine (Unofficial)

Minimal rethinkdb docker images based on alpine linux.

## Versions

### :latest (~36MB)

- Based on [alpine:3.15](https://hub.docker.com/_/alpine)
- Uses rethinkdb 2.4.2 built [from source](https://github.com/rethinkdb/rethinkdb)

### :python (~79MB)

- Based on [python3.10-alpine3.15](https://hub.docker.com/_/python)
- Includes the [rethinkdb python driver](https://rethinkdb.com/docs/install-drivers/python/)
- Uses rethinkdb binary from [besworks/rethinkdb:latest](https://hub.docker.com/layers/208153988/besworks/rethinkdb/latest/images/sha256-06beb4966c6f8c8847d4ae268f1e36822af87038e90fc3bf9d65f693cbcfda9c?context=repo)

## Usage

Building **:latest** from it's Dockerfile takes some time and produces a rather large intermediary build image (~3GB). It's recommended to pull this version [from docker hub](https://hub.docker.com/repository/docker/besworks/rethinkdb) unless you are forking this project for research/development.

```
docker run -d --name=rdbtest -p 8080:8080 -p 28015:28015 -p 29015:29015 besworks/rethinkdb:latest

docker logs -f rdbtest

docker stop rdbtest
```

