FROM node:alpine
MAINTAINER "Carter Mbotho <carter@suilteam.com>"

RUN npm install -g mocha chai chai-http mocha-junit-reporter

RUN adduser -s /bin/sh -h /home/suiltest -D suiltest

WORKDIR /home/suiltest
