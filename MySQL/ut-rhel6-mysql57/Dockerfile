FROM redhat/ut-rhel6rhs

MAINTAINER Rick Huff <rhuff@austin.utexas.edu>

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r mysql && useradd -r -g mysql mysql

RUN mkdir /docker-entrypoint-initdb.d

RUN yum update && yum install -y mysql-server
RUN chown -R mysql /var/lib/mysql && chgrp -R mysql /var/lib/mysql && mysql_install_db --user=mysql -ldata=/var/lib/mysql
RUN mysqld_safe & \
    sleep 10s &&\
    echo "GRANT ALL ON *.* TO root@'%' WITH GRANT OPTION; FLUSH PRIVILEGES" | mysql

COPY docker-entrypoint.sh /entrypoint.sh
RUN chmod 755 /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 3306
# CMD ["mysqld_safe"]
CMD ["/bin/bash"]


