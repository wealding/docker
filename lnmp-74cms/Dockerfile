FROM index.tenxcloud.com/bagheera/lnmp
MAINTAINER bagheera "ding@gong.si"

# set timezone to PRC
RUN mv /etc/localtime /etc/localtime.bak
RUN ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

ADD chinese-sources.list /etc/apt/sources.list

RUN apt-get update && apt-get install -y wget unzip && rm -rf /var/lib/apt/lists/*

ENV 74CMS_VERSION 3.6_20150923

# 下载phpcms
RUN wget -O 74cms.zip http://download.74cms.com/download/74cms_v3.6_20150923.zip
RUN unzip -d 74cms/ ./74cms.zip
RUN rm -rf /usr/share/nginx/html/*
RUN cp -rf 74cms/74cms_v3.6_20150923/upload/. /usr/share/nginx/html
RUN mkdir /usr/share/nginx/html/html
RUN chmod -R 777 /usr/share/nginx/html/data /usr/share/nginx/html/temp /usr/share/nginx/html/html /usr/share/nginx/html/templates /usr/share/nginx/html/admin/statement /usr/share/nginx/html/install
RUN rm -rf ./74cms*

EXPOSE 80 3306

ADD default.conf /etc/nginx/conf.d/default.conf

CMD /run.sh