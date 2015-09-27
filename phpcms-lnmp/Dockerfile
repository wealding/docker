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
RUN rm -fr /home/wwwroot/default/*
RUN cp -r phpcms/install_package /home/wwwroot/default
RUN rm -fr ./phpcms*


EXPOSE 80 3306

CMD service php5-fpm start && nginx -g "daemon off;" && mysqld