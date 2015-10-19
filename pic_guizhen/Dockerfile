FROM index.tenxcloud.com/bagheera/nginx_php5
MAINTAINER bagheera "ding@gong.si"

ADD chinese-sources.list /etc/apt/sources.list

# set timezone to PRC
RUN mv /etc/localtime /etc/localtime.bak
RUN ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo "nameserver 114.114.114.114" >> /etc/resolv.conf
RUN echo "nameserver 119.29.29.29" >>  /etc/resolv.conf

# Add VOLUMEs to allow backup of config and databases
VOLUME  ["/usr/share/nginx/html"]

EXPOSE 80

# Enable php by default
ADD default.conf /etc/nginx/conf.d/default.conf

RUN sed -i 's/server_names_hash_bucket_size 32/server_names_hash_bucket_size 64/g' /etc/nginx/nginx.conf
CMD service php5-fpm start && nginx -g "daemon off;"