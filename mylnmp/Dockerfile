FROM index.tenxcloud.com/bagheera/lnmp
MAINTAINER bagheera "ding@gong.si"

# set timezone to PRC
RUN mv /etc/localtime /etc/localtime.bak
RUN ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

ADD chinese-sources.list /etc/apt/sources.list
RUN apt-get update && apt-get install -y wget vim dnsutils curl dnsmasq && rm -rf /var/lib/apt/lists/*

# DNSMASQ
RUN echo "">>/etc/dnsmasq.conf
RUN echo "user=root">>/etc/dnsmasq.conf
RUN echo "listen-address=127.0.0.1">>/etc/dnsmasq.conf

VOLUME  ["/mydata"]

RUN chmod -R 777 /mydata

EXPOSE 80 3306

RUN ln -sf /mydata/conf/default.conf /etc/nginx/conf.d/default.conf
RUN ln -sf /mydata/conf/avatar.conf /etc/nginx/conf.d/avatar.conf
RUN ln -sf /mydata/conf/nginx.conf /etc/nginx/nginx.conf
RUN ln -sf /mydata/conf/phpfpm-www.conf /etc/php5/fpm/pool.d/www.conf

CMD /run.sh