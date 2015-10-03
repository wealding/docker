FROM index.tenxcloud.com/bagheera/nginx_php5
MAINTAINER bagheera "ding@gong.si"

ADD chinese-sources.list /etc/apt/sources.list

# Add MySQL configuration
ADD my.cnf /etc/mysql/conf.d/my.cnf
ADD mysqld_charset.cnf /etc/mysql/conf.d/mysqld_charset.cnf

RUN apt-get update
RUN apt-get -y install pwgen

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q mysql-server && \
    rm -rf /var/lib/apt/lists/* && \
    if [ ! -f /usr/share/mysql/my-default.cnf ] ; then cp /etc/mysql/my.cnf /usr/share/mysql/my-default.cnf; fi && \
    mysql_install_db > /dev/null 2>&1 && \
    touch /var/lib/mysql/.EMPTY_DB

# Add MySQL scripts
ADD import_sql.sh /import_sql.sh
ADD run.sh /run.sh
RUN chmod +x /*.sh

ENV MYSQL_USER=admin \
    MYSQL_PASS=**Random** \
    ON_CREATE_DB=**False** \
    REPLICATION_MASTER=**False** \
    REPLICATION_SLAVE=**False** \
    REPLICATION_USER=replica \
    REPLICATION_PASS=replica

# set timezone to PRC
RUN mv /etc/localtime /etc/localtime.bak
RUN ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo "nameserver 114.114.114.114" >> /etc/resolv.conf
RUN echo "nameserver 119.29.29.29" >>  /etc/resolv.conf

# change max_upload size
RUN sed -i "s/http {/http {\n        client_max_body_size 80M;/" /etc/nginx/nginx.conf
RUN sed -i "s/upload_max_filesize = 2M/upload_max_filesize = 80M/" /etc/php5/fpm/php.ini
RUN sed -i "s/post_max_size = 8M/post_max_size = 80M/" /etc/php5/fpm/php.ini


# Add VOLUMEs to allow backup of config and databases
VOLUME  ["/etc/mysql", "/var/lib/mysql", "/usr/share/nginx/html"]

EXPOSE 80 3306

CMD /run.sh