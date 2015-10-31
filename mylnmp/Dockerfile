FROM index.tenxcloud.com/bagheera/lnmp
MAINTAINER bagheera "ding@gong.si"

# set timezone to PRC
RUN mv /etc/localtime /etc/localtime.bak
RUN ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
# set DNS
RUN echo "nameserver 114.114.114.114" > /etc/resolv.conf
RUN echo "nameserver 192.168.1.53" >>  /etc/resolv.conf
RUN echo "nameserver 10.16.40.3" >>  /etc/resolv.conf
RUN echo "nameserver 1.2.4.8" >>  /etc/resolv.conf
RUN echo "search bagheera.svc.tenx.local svc.tenx.local tenx.local pek2.qingcloud.com" >>  /etc/resolv.conf
RUN echo "options ndots:5" >>  /etc/resolv.conf

ADD chinese-sources.list /etc/apt/sources.list
RUN apt-get update && apt-get install -y wget && rm -rf /var/lib/apt/lists/*

VOLUME  ["/mydata"]

RUN chmod -R 777 /mydata

EXPOSE 80 3306

RUN ln -sf /mydata/conf/default.conf /etc/nginx/conf.d/default.conf

CMD /run.sh