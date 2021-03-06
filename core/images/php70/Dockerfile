FROM node:8.16.0-alpine

MAINTAINER peter <peter@xulukun.cn>

# Mirror mirror switch to Ali-OSM (Alibaba Open Source Mirror Site) - http://mirrors.aliyun.com/
RUN echo 'https://mirrors.aliyun.com/alpine/v3.5/main' > /etc/apk/repositories  && \
	echo 'https://mirrors.aliyun.com/alpine/v3.5/community' >> /etc/apk/repositories
	# && echo "http://dl-4.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

# ensure www-data user exists
RUN set -x \
	&& addgroup -g 1100 -S www-data \
	&& adduser -u 1100 -D -S -G www-data www-data
# 1100 is the standard uid/gid for "www-data" in Alpine

RUN apk update && apk upgrade && \
    apk add --update --no-cache \
        curl \
        php7 \
        php7-common \
        php7-fpm \
        php7-dom \
        php7-mbstring \
        php7-json \
        php7-bcmath \
        php7-ctype \
        php7-curl \ 
        php7-gd \ 
        php7-intl \
        php7-mcrypt \
        php7-openssl \
        php7-pdo \
        php7-pdo_mysql \
        php7-pdo_sqlite \
        php7-soap \
        php7-xsl \ 
        php7-zip \
        php7-iconv \
        php7-phar \ 
        php7-opcache \
        php7-session \
        php7-xml \
        php7-ftp \
# git
        git \
# git ssh
        bash \
        openssh && \
# Cleaning up
    rm -rf /var/cache/apk/*

RUN npm install -g cnpm --registry=https://registry.npm.taobao.org && \
    yarn config set registry https://registry.npm.taobao.org && \
    cnpm i -g grunt-cli gulp-cli

# Set Workdir
WORKDIR /var/www/html

# Expose ports
EXPOSE 9070

# Entry point
CMD ["/usr/sbin/php-fpm7", "-R", "--nodaemonize"]