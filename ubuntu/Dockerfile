FROM ubuntu:latest

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y cmake sqlite3 libsqlite3-dev \
                       libpq-dev postgresql postgresql-server-dev-all   \
                       uuid-dev openssl1.0 libssl1.0-dev build-essential
