FROM ubuntu:latest

RUN apt-get clean && apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --fix-missing cmake sqlite3 libsqlite3-dev \
                       libpq-dev postgresql postgresql-server-dev-all   \
                       uuid-dev openssl1.0 libssl1.0-dev build-essential \
                       autoconf automake libtool curl make unzip wget
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y openssh-server nano rsync gdb lua5.3 bsdmainutils

RUN export CXXFLAGS=-fPIC && mkdir -p /tmp/protoc && cd /tmp/protoc && \
    wget https://github.com/protocolbuffers/protobuf/releases/download/v3.7.0/protobuf-all-3.7.0.zip && \
    unzip protobuf-all-3.7.0.zip && cd protobuf-3.7.0 && \
    ./autogen.sh && ./configure --enable-shared=no --enable-static=yes --prefix=/usr/local/ && \
    make -j5 && make install && cd && rm -rf /tmp/protoc && rm -rf /usr/local/lib/libprotobuf.* && \
    rm -rf /usr/local/libprotoc.*

# Setup ssh for remote debugging
RUN ln -s /usr/bin/lua5.3 /usr/local/bin/lua ; ln -s /usr/bin/luac5.3 /usr/bin/local/luac
RUN mkdir /var/run/sshd
RUN echo 'root:build' | chpasswd
RUN sed -i 's/.*PermitRootLogin.*/PermitRootLogin yes/g' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profiles"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

