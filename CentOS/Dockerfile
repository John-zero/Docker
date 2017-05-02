#
FROM centos:latest

#
MAINTAINER by John_zero (2625210655@qq.com)

#
RUN yum makecache fast && yum -y update glibc

RUN yum clean all 
RUN yum install -y yum-plugin-ovl || true
RUN yum install -y vim tar wget curl rsync bzip2 iptables tcpdump less telnet net-tools lsof sysstat cronie python-setuptools
RUN yum clean all

RUN easy_install supervisor

RUN cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN mkdir -p /etc/supervisor/conf.d/
RUN /usr/bin/echo_supervisord_conf > /etc/supervisord.conf
RUN echo [include] >> /etc/supervisord.conf
RUN echo 'files = /etc/supervisor/conf.d/*.conf' >> /etc/supervisord.conf

COPY sshd.conf /etc/supervisor/conf.d/sshd.conf

# 
EXPOSE 22

#
CMD ["/usr/bin/supervisord"]