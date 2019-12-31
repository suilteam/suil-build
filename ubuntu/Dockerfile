FROM ubuntu:latest

# Install all required packages
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y cmake sqlite3 libsqlite3-dev \
                       libpq-dev postgresql postgresql-server-dev-all   \
                       uuid-dev openssl1.0 libssl1.0-dev build-essential \
                       autoconf automake libtool curl make unzip wget libzmq3-dev git

# Build secp256k1 and install in image
RUN git clone https://github.com/bitcoin-core/secp256k1.git /tmp/secp256k1 && \
     cd /tmp/secp256k1 && ./autogen.sh && ./configure CPPFLAGS='-fPIC' CFLAGS='-fPIC' --enable-shared=no --enable-static=yes --enable-module-recovery && \
     make -j3 && make install && cd && rm -rf /tmp/secp256k1

# Build protobuf library and install
RUN export CXXFLAGS=-fPIC && mkdir -p /tmp/protoc && cd /tmp/protoc && \
    wget https://github.com/protocolbuffers/protobuf/releases/download/v3.7.0/protobuf-all-3.7.0.zip && \
    unzip protobuf-all-3.7.0.zip && cd protobuf-3.7.0 && \
    ./autogen.sh && ./configure --enable-shared=no --enable-static=yes --prefix=/usr/local/ && \
    make -j5 && make install && cd && rm -rf /tmp/protoc && rm -rf /usr/local/lib/libprotobuf.*

