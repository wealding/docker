FROM debian:jessie
MAINTAINER bagheera "ding@gong.si"

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
RUN echo "deb http://nginx.org/packages/mainline/debian/ jessie nginx" >> /etc/apt/sources.list

ENV NGINX_VERSION 1.9.5-1~jessie

RUN apt-get update && \
    apt-get install -y ca-certificates nginx=${NGINX_VERSION} && \
    rm -rf /var/lib/apt/lists/*

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME ["/var/cache/nginx"]

EXPOSE 80

# set timezone to PRC
RUN mv /etc/localtime /etc/localtime.bak
RUN ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN apt-get update -y && apt-get install -y php5-fpm php5-curl php5-memcache php5-sqlite php5-tidy php5-xmlrpc php5-mcrypt php5-mhash php5-intl php-apc php5-gd php5-intl php5-mysqlnd php5-pgsql php-pear php5-cli && rm -rf /var/lib/apt/lists/*

# Once we start using PHP, it will dictate the use of www-data, so use that instead of nginx
RUN sed -i 's/user  nginx/user  www-data/g' /etc/nginx/nginx.conf

# Force PHP to log to nginx
RUN echo "catch_workers_output = yes" >> /etc/php5/fpm/php-fpm.conf

# Enable php by default
ADD default.conf /etc/nginx/conf.d/default.conf

CMD service php5-fpm start && nginx -g "daemon off;"