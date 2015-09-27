FROM index.tenxcloud.com/bagheera/lnmp
MAINTAINER bagheera "ding@gong.si"

# set timezone to PRC
RUN mv /etc/localtime /etc/localtime.bak
RUN ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

ADD chinese-sources.list /etc/apt/sources.list

RUN apt-get update && apt-get install -y wget unzip && rm -rf /var/lib/apt/lists/*

ENV PHPCMS_VERSION 9.5.10

# 下载phpcms
RUN wget -O phpcms.zip http://download.phpcms.cn/v9/9.5/phpcms_v9.5.10_UTF8.zip
RUN unzip -d phpcms/ ./phpcms.zip
RUN rm -rf /usr/share/nginx/html/*
RUN cp -rf phpcms/install_package/. /usr/share/nginx/html
RUN chmod -R 777 /usr/share/nginx/html/index.html /usr/share/nginx/html/caches /usr/share/nginx/html/html /usr/share/nginx/html/uploadfile /usr/share/nginx/html/phpsso_server/caches /usr/share/nginx/html/phpsso_server/uploadfile
RUN rm -rf ./phpcms*

EXPOSE 80 3306

CMD service php5-fpm start && nginx -g "daemon off;" && mysqld