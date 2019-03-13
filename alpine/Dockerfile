FROM n0madic/alpine-gcc:7.3.0
MAINTAINER "Carter Mbotho"

RUN apk update
RUN apk add curl git openssh bash sqlite sqlite-dev && \
    apk add openssl libressl-dev postgresql-dev && \
    apk add bsd-compat-headers util-linux-dev && \
    apk add libressl2.7-libcrypto docker && \
    apk add autoconf automake libtool curl make unzip
    
RUN L=/usr/local/bin/flynn && curl -sSL -A "`uname -sp`" https://dl.flynn.io/cli | zcat >$L && chmod +x $L

RUN mkdir -p /tmp/protoc && cd /tmp/protoc && \
    wget https://github.com/protocolbuffers/protobuf/releases/download/v3.7.0/protobuf-all-3.7.0.zip && \
    unzip protobuf-all-3.7.0.zip && cd protobuf-3.7.0 && \
    ./autogen.sh && ./configure --enable-shared=no --enable-static=yes --prefix=/usr/local/ && \
    make -j5 && make install && cd && rm -rf /tmp/protoc && rm -rf /usr/local/lib/libprotobuf.* && \
    rm -rf /usr/local/libprotoc.*
