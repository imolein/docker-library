FROM alpine:3.11

LABEL maintainer="Sebastian Huebner <sh@kokolor.es>"

ENV LUA_VERSION=5.4.0

RUN set -ex \
    \
    && apk add readline-dev \
    && apk add --no-cache --virtual .build-deps \
        make \
        gcc \
        libc-dev \
    \
    && wget -c https://www.lua.org/work/lua-${LUA_VERSION}-rc1.tar.gz \
        -O - | tar -xzf - \
    \
    && cd lua-${LUA_VERSION} \
    && make -j"$(nproc)" linux-readline \
    && make install \
    && cd .. \
    && rm -rf lua-${LUA_VERSION} \
    \
    && apk del .build-deps

CMD ["lua"]