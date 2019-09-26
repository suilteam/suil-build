FROM node:alpine
MAINTAINER "Carter Mbotho <carter@suilteam.com>"

RUN npm install -g mocha && npm install -g chai && \
    npm install -g chai-http && npm install -g mocha-junit-reporter

RUN adduser -s /bin/sh -h /home/suiltest -D suiltest

WORKDIR /home/suiltest
