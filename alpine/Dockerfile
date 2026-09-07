FROM alpine:3.22

ARG NSIS_VERSION=3.12
ARG NSIS_SOURCE_HASH=f3ed7a8e4aa2cf4e8cf47d3b563a02559e0cb4934db2662b2f9661b824e2b186

ENV NSIS_SOURCE_URL="https://sourceforge.net/projects/nsis/files/NSIS%203/${NSIS_VERSION}/nsis-${NSIS_VERSION}-src.tar.bz2/download"

RUN apk add --no-cache --virtual .build-deps \
        build-base \
        bzip2 \
        ca-certificates \
        curl \
        gnu-libiconv-dev \
        i686-mingw-w64-gcc \
        scons \
        unzip \
        zlib-dev \
    && mkdir -p /usr/src/nsis \
    && curl -fsSL "$NSIS_SOURCE_URL" -o /tmp/nsis.tar.bz2 \
    && echo "$NSIS_SOURCE_HASH  /tmp/nsis.tar.bz2" | sha256sum -c - \
    && tar -xjf /tmp/nsis.tar.bz2 --strip-components=1 -C /usr/src/nsis \
    && mkdir /tmp/zlib \
    && curl -fsSL 'https://downloads.sourceforge.net/project/libpng/zlib/1.2.8/zlib128-dll.zip?r=&ts=1403402496&use_mirror=hivelocity' -o /tmp/zlib.zip \
    && unzip -q /tmp/zlib.zip -d /tmp/zlib \
    && cd /usr/src/nsis \
    && scons ZLIB_W32=/tmp/zlib APPEND_CPPPATH=/usr/include/gnu-libiconv SKIPPLUGINS=all \
    && scons ZLIB_W32=/tmp/zlib APPEND_CPPPATH=/usr/include/gnu-libiconv SKIPPLUGINS=all install PREFIX=/usr/local \
    && install -Dm755 build/urelease/makensis/makensis /usr/local/bin/makensis \
    && apk del .build-deps \
    && apk add --no-cache gnu-libiconv-libs libgcc libstdc++ \
    && rm -rf /usr/src/nsis /tmp/nsis.tar.bz2

WORKDIR /installer
ENTRYPOINT ["makensis"]
