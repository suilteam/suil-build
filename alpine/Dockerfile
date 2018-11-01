FROM n0madic/alpine-gcc:7.3.0
MAINTAINER "Carter Mbotho"

RUN apk update
RUN apk add curl git openssh bash sqlite sqlite-dev && \
    apk add openssl libressl-dev postgresql-dev && \
    apk add bsd-compat-headers util-linux-dev && \
    apk add libressl2.7-libcrypto docker
    
RUN L=/usr/local/bin/flynn && curl -sSL -A "`uname -sp`" https://dl.flynn.io/cli | zcat >$L && chmod +x $L
