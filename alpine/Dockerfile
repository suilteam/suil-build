FROM alpine:latest
MAINTAINER "Carter Mbotho"

RUN apk update
RUN apk add curl git openssh bash cmake sqlite sqlite-dev && \
    apk add openssl libressl-dev postgresql-dev && \
    apk add bsd-compat-headers gcc g++ make util-linux-dev && \
    apk add protobuf-dev libressl2.6-libcrypto docker
    
RUN L=/usr/local/bin/flynn && curl -sSL -A "`uname -sp`" https://dl.flynn.io/cli | zcat >$L && chmod +x $L
