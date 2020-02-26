FROM suilteam/mecury:ubuntu

# Setup ssh for remote debugging
RUN ln -s /usr/bin/lua5.3 /usr/local/bin/lua ; ln -s /usr/bin/luac5.3 /usr/local/bin/luac
RUN mkdir /var/run/sshd
RUN echo 'root:build' | chpasswd
RUN sed -i 's/.*PermitRootLogin.*/PermitRootLogin yes/g' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profiles"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

