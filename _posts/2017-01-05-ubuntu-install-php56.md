---
title: ubuntu 编译安装php5.6
category: yii2
author: 酱油先生
---

```shell
sudo apt-get install openssl 
sudo apt-get install libssl-dev 
apt-get install make
apt-get install curl
apt-get install libcurl4-gnutls-dev


sudo apt-get install libjpeg-dev


sudo apt-get install libpng-dev


sudo apt-get install libmcrypt-dev


sudo apt-get install libreadline6 libreadline6-dev




sudo ./configure \
--prefix=/usr/local/php56 \
--with-mysql=mysqlnd \
--with-mysqli=mysqlnd \
--with-pdo-mysql=mysqlnd \
--with-config-file-path=/etc/php56 \
--with-zlib \
--with-curl \
--with-curlwrappers \
--with-mcrypt \
--with-gd \
--with-openssl \
--with-mhash \
--with-xmlrpc \
--with-jpeg-dir \
--with-png-dir \
--with-xpm-dir \
--with-freetype-dir \
--with-zlib-dir \
--enable-shared \
--enable-fpm \
--enable-xml \
--disable-rpath \
--enable-safe-mode \
--enable-bcmath \
--enable-shmop \
--enable-sysvsem \
--enable-inline-optimization \
--enable-mbregex \
--enable-mbstring \
--enable-gd-native-ttf \
--enable-pcntl \
--enable-sockets \
--enable-zip \
--enable-soap

```
