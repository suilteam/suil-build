FROM alpine:latest
MAINTAINER "Carter Mbotho"

RUN apk update
RUN apk add openssh bash cmake sqlite sqlite-dev && \
    apk add openssl libressl-dev postgresql-dev && \
    apk add bsd-compat-headers gcc g++ make util-linux-dev
