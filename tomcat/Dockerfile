# 定义镜像版本
ARG TOMCAT_VERSION
FROM tomcat:${TOMCAT_VERSION}

LABEL maintainer="Zou You <hellozouyou@gmail.com>"

COPY ./conf/server.xml /usr/local/tomcat/conf/

# Change application source from dl-cdn.alpinelinux.org to aliyun source
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories

RUN apk update \
  && apk upgrade \
  && apk add --no-cache openssl \
  && apk add --no-cache bash \
  && adduser -D -H -u 1000 -s /bin/bash www-data

EXPOSE 80 443
