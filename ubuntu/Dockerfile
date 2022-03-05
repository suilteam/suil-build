FROM ubuntu:latest

# Install all required packages
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y gnupg2

RUN DEBIAN_FRONTEND=noninteractive . /etc/os-release && \
     echo "deb http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu $UBUNTU_CODENAME main" > /etc/apt/sources.list.d/ubuntu-toolchain-r-ubuntu-test-focal.list && \
     apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1E9377A2BA9EF27F && \
     apt-get update

RUN DEBIAN_FRONTEND=noninteractive \
     apt-get install -y cmake sqlite3 libsqlite3-dev libpq-dev postgresql postgresql-server-dev-all   \
     uuid-dev openssl libssl-dev dpkg-dev libc6-dev make autoconf automake libtool curl make unzip wget \
     openssh-server nano rsync gdb bsdmainutils libzmq3-dev git flex bison && \
     apt-get purge -y gcc-9 g++-9 && \
     apt-get autoremove -y && \
     apt-get install -y gcc-11 g++-11 gcc-11-plugin-dev && \
     update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 10 && \
     update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 10


# Build secp256k1 and install in image
RUN git clone https://github.com/bitcoin-core/secp256k1.git /tmp/secp256k1 && \
     cd /tmp/secp256k1 && ./autogen.sh && ./configure CPPFLAGS='-fPIC' CFLAGS='-fPIC' --enable-shared=no --enable-static=yes --enable-module-recovery && \
     make -j3 && make install && cd && rm -rf /tmp/secp256k1

# Build protobuf library and install
RUN export CXXFLAGS=-fPIC && mkdir -p /tmp/protoc && cd /tmp/protoc && \
    wget https://github.com/protocolbuffers/protobuf/releases/download/v3.7.0/protobuf-all-3.7.0.zip && \
    unzip protobuf-all-3.7.0.zip && cd protobuf-3.7.0 && \
    ./autogen.sh && ./configure --enable-shared=no --enable-static=yes --prefix=/usr/local/ && \
    make -j5 && make install && cd && rm -rf /tmp/protoc

# Build lua and install library
RUN export CXXFLAGS=-fPIC && cd /tmp && \
    curl -R -O http://www.lua.org/ftp/lua-5.4.3.tar.gz &&   \
    tar zxf lua-5.4.3.tar.gz && \
    cd lua-5.4.3 && \
    make && make install && \
    cd /tmp && rm -rf lua-*
