FROM besworks/rethinkdb:latest AS rdb

FROM python:3.10-alpine3.15 AS rdbtools
ARG RUN_DEPS="ca-certificates libstdc++ libgcc libcurl protobuf libexecinfo"
ARG RUN_AS=rethinkdb
ARG DATA_DIR=/data

WORKDIR /usr/bin
RUN apk add --no-cache --update ${RUN_DEPS}
COPY --from=rdb /usr/bin/rethinkdb ./

WORKDIR ${DATA_DIR}
RUN adduser -D ${RUN_AS} \
&& chown -R ${RUN_AS}:${RUN_AS} ./

USER ${RUN_AS}
ENV PATH=${PATH}:/home/${RUN_AS}/.local/bin
RUN python3 -m ensurepip
RUN pip3 install rethinkdb

ENTRYPOINT rethinkdb --bind all --directory ./

EXPOSE 28015 29015 8080
