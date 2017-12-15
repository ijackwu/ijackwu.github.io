---
title: 'php5.6 sqlsrv x64 无法装'
categories: php
author: "酱油先生"
---

今天配置服务器需要用PHP和Sqlserver2008数据库，网上找了一些资料，基本上都是说需要下载微软的驱动放在ext文件夹后，再在php.ini中增加如下配置：
```
[PHP_PDO_SQLSRV] 
extension=php_pdo_sqlsrv_56_nts.dll 
[PHP_SQLSRV] 
extension=php_sqlsrv_56_nts.dll 
```

原来微软官方提供的microsoft drivers 3.2 for php for sql server并不支持64位的php版本,一些非官方的3.0.2.2倒是单独提供了64位版本的编译，有热心网友提供了百度的分享，
http://pan.baidu.com/s/1dDIRpJF


