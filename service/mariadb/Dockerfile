FROM centos:7
MAINTAINER Li Hao <lihao@me.com>
ADD MariaDB.repo /etc/yum.repos.d/
RUN chmod 775 /etc/yum.repos.d/MariaDB.repo
RUN yum update
RUN yun -y upgrade
RUN yum -y install pwgen
RUN yum -y install MariaDB-server
RUN rm -rf /var/lib/mysql/*
ADD create_mariadb_admin_user.sh /create_mariadb_admin_user.sh
ADD run.sh /run.sh
RUN chmod 775 /*.sh

VOLUME ["/etc/mysql", "/var/lib/mysql"]

ENV TERM dumb

EXPOSE 3306
CMD ["/run.sh"]