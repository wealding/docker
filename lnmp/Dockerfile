FROM index.tenxcloud.com/bagheera/nginx_php5
MAINTAINER bagheera "ding@gong.si"

ADD chinese-sources.list /etc/apt/sources.list

RUN mkdir /mysqldata

# Install MySQL 5.6
RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update && apt-get install -y --force-yes \
    mysql-server-5.6 && \
    service mysql stop && \
    sed -e 's/^datadir\t.*$/datadir = \/mysqldata/' -i /etc/mysql/my.cnf && \
    sed -e 's/^bind-address\t.*$/bind-address = 0.0.0.0/' -i /etc/mysql/my.cnf && \
    cp /etc/mysql/my.cnf /usr/share/mysql/my-default.cnf && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Add scripts
ADD firstrun.sh firstrun.sh
RUN chmod +x *.sh
RUN firstrun.sh

# Expose our data directory
VOLUME ["/mysqldata", "/var/log/mysql", "/etc/mysql"]

EXPOSE 3306

CMD service php5-fpm start && nginx -g "daemon off;" && /usr/sbin/mysqld