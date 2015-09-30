FROM index.tenxcloud.com/bagheera/lnmp
MAINTAINER bagheera "ding@gong.si"

# set timezone to PRC
RUN mv /etc/localtime /etc/localtime.bak
RUN ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo "nameserver 114.114.114.114" >> /etc/resolv.conf
RUN echo "nameserver 119.29.29.29" >>  /etc/resolv.conf

ADD chinese-sources.list /etc/apt/sources.list
RUN apt-get update && apt-get install -y wget && rm -rf /var/lib/apt/lists/*

ENV MAX_UPLOAD "80M"

ADD dingfm.php /usr/share/nginx/html/dingfm.php
RUN chmod -R 777 /usr/share/nginx/html

RUN sed -i "s/upload_max_filesize = 2M/upload_max_filesize = $MAX_UPLOAD/" /etc/php5/fpm/php.ini
RUN sed -i "s/post_max_size = 8M/post_max_size = $MAX_UPLOAD/" /etc/php5/fpm/php.ini


EXPOSE 80 3306

ADD default.conf /etc/nginx/conf.d/default.conf

CMD /run.sh