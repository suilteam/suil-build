FROM alpine:edge
LABEL author="Carter Mbotho"

RUN apk upgrade --available

# Install required packages
RUN apk add --no-cache \
            curl git openssh bash sqlite sqlite-dev \
            openssl libressl-dev postgresql-dev \
            bsd-compat-headers util-linux-dev zeromq-dev \
            docker autoconf automake libtool curl make unzip wget \
            gcc g++ cmake flex bison

# Build secp256k1 and install in image
RUN git clone https://github.com/bitcoin-core/secp256k1.git /tmp/secp256k1 && \
    cd /tmp/secp256k1 && ./autogen.sh && ./configure CPPFLAGS='-fPIC' CFLAGS='-fPIC' --enable-shared=no --enable-static=yes --enable-module-recovery && \
    make -j3 && make install && cd && rm -rf /tmp/secp256k1

# Build protobuf and install
RUN export CXXFLAGS=-fPIC && mkdir -p /tmp/protoc && cd /tmp/protoc && \
    wget https://github.com/protocolbuffers/protobuf/releases/download/v3.7.0/protobuf-all-3.7.0.zip && \
    unzip protobuf-all-3.7.0.zip && cd protobuf-3.7.0 && \
    ./autogen.sh && ./configure --enable-shared=no --enable-static=yes --prefix=/usr/local/ && \
    make -j5 && make install && cd && rm -rf /tmp/protoc && rm -rf /usr/local/libprotoc.*

# Build lua and install library
RUN export CXXFLAGS=-fPIC && cd /tmp && \
    curl -R -O http://www.lua.org/ftp/lua-5.4.3.tar.gz &&   \
    tar zxf lua-5.4.3.tar.gz && \
    cd lua-5.4.3 && \
    make && make install && \
    cd /tmp && rm -rf lua-*
