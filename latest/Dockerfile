FROM alpine:3.16 AS base

FROM base AS build
ARG RETHINKDB_PACKAGE_VERSION=2.4.3
ARG SOURCE_PATH=https://download.rethinkdb.com/repository/raw/dist/
ARG SOURCE_BASE=rethinkdb-${RETHINKDB_PACKAGE_VERSION}
ARG SOURCE_EXT=.tgz
ARG BUILD_DEPS="bash linux-headers bsd-compat-headers m4 g++ make python3 protobuf-dev icu-dev libressl-dev curl-dev boost-dev libexecinfo-dev"
ARG FLAGS_CONF="--dynamic all --prefix=/usr --sysconfdir=/etc --localstatedir=/var"
ARG FLAGS_CXX="-fno-delete-null-pointer-checks"
ARG FLAGS_LD="-lexecinfo"

RUN apk add --no-cache --update ${BUILD_DEPS} \
&& ln -sf python3 /usr/bin/python

ENV BUILD_DIR=/tmp/build
ENV SOURCE_FILE=${SOURCE_BASE}${SOURCE_EXT}
ENV SOURCE_URL=${SOURCE_PATH}${SOURCE_FILE}
WORKDIR ${BUILD_DIR}
RUN wget ${SOURCE_URL}
RUN tar -xzf ${SOURCE_FILE}

ENV CXXFLAGS=${FLAGS_CXX}
ENV LDFLAGS=${FLAGS_LD}
WORKDIR ${BUILD_DIR}/${SOURCE_BASE}
RUN ./configure ${FLAGS_CONF} \
&& make SPLIT_SYMBOLS=1
RUN make install-binaries STRIP_ON_INSTALL=1
	
FROM base AS rethinkdb
ARG RUN_DEPS="ca-certificates libstdc++ libgcc libcurl protobuf libexecinfo"
ARG RUN_AS=rethinkdb
ARG DATA_DIR=/data

WORKDIR /usr/bin
RUN apk add --no-cache --update ${RUN_DEPS}
COPY --from=build /usr/bin/rethinkdb ./

WORKDIR ${DATA_DIR}
RUN adduser -D ${RUN_AS} \
&& chown -R ${RUN_AS}:${RUN_AS} ./
USER ${RUN_AS}
ENTRYPOINT rethinkdb --bind all --directory ./
EXPOSE 28015 29015 8080
