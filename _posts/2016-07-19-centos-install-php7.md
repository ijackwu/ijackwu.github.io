---
title:centos7 php7编译安装
category: php
---

## 下载安装包 php-7.0.8.tar.bz2

```
wget http://cn2.php.net/get/php-7.0.8.tar.bz2/from/this/mirror -O php-7.0.8.tar.bz2
```

## 依赖环境
```
yum -y install epel-release
yum -y install libxml2 libxml2-devel openssl openssl-devel curl-devel libjpeg-devel libpng-devel freetype-devel libmcrypt-devel
```

## 编译安装php7
```
tar -xvf php-7.0.8.tar.bz2
cd php-7.0.8

./configure --prefix=/usr/local/php7 \
--with-config-file-path=/usr/local/php7/etc \
--with-config-file-scan-dir=/usr/local/php7/etc/php.d \
--with-mcrypt=/usr/include \
--enable-mysqlnd \
--with-mysqli \
--with-pdo-mysql \
--enable-fpm \
--with-fpm-user=nginx \
--with-fpm-group=nginx \
--with-gd \
--with-iconv \
--with-zlib \
--enable-xml \
--enable-shmop \
--enable-sysvsem \
--enable-inline-optimization \
--enable-mbregex \
--enable-mbstring \
--enable-ftp \
--enable-gd-native-ttf \
--with-openssl \
--enable-pcntl \
--enable-sockets \
--with-xmlrpc \
--enable-zip \
--enable-soap \
--without-pear \
--with-gettext \
--enable-session \
--with-curl \
--with-jpeg-dir \
--with-freetype-dir \
--enable-opcache


make -j `grep processor /proc/cpuinfo | wc -l`
make install
```

## 修改配置文件

```
cp php.ini-development /usr/local/php7/etc/

添加配置
zend_extension=opcache.so
opcache.enable=1
opcache.enable_cli=1
opcache.huge_code_pages=1
opcache.file_cache=/tmp


cp sapi/fpm/init.d.php-fpm /etc/init.d/php7-fpm
sudo chmod +x /etc/init.d/php7-fpm

cd /usr/local/php7/etc
cp php-fpm.conf.default php-fpm.conf
cd php-fpm.d/
cp www.conf.default www.conf
```

## 添加 php-intl 扩展

```
cd php-7.0.8/ext/intl
/usr/local/php7/bin/phpize

// 添加依赖

 yum install icu libicu-devel

./configure --with-php-config=/usr/local/php7/bin/php-config

 make && make install 

添加扩展到php.ini
extension=intl.so
```

## 添加到启动项目

```
systemctl enable php7-fpm
 systemctl start php7-fpm
```

## 查看是否正常

```
[root@localhost etc]# ps -ef | grep php-
root     10132     1  0 13:19 ?        00:00:00 php-fpm: master process (/usr/local/php7/etc/php-fpm.conf)
nginx    10133 10132  0 13:19 ?        00:00:00 php-fpm: pool www
nginx    10134 10132  0 13:19 ?        00:00:00 php-fpm: pool www
```

