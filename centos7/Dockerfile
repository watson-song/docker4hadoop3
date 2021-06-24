FROM centos:7
MAINTAINER sow(watson.song@gmail.com)

RUN yum install -y openssh-server sudo
RUN echo 'PermitRootLogin yes' >> /etc/ssh/sshd_config
RUN yum install -y openssh-clients

RUN echo "root:qwe123" | chpasswd
RUN echo "root    ALL=(ALL)     ALL" >> /etc/sudoers
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key

RUN mkdir /var/run/sshd
EXPOSE 22
CMD ["/usr/sbin/sshd","-D"]