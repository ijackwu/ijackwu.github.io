---
title: "Composer OpenSSL Error messages for window"
category: "php"
---

## 错误提示

```
[Composer\Downloader\TransportException]
 The "https://getcomposer.org/version" file could not be downloaded: SSL ope
 ration failed with code 1. OpenSSL Error messages:
 error:14090086:SSL routines:SSL3_GET_SERVER_CERTIFICATE:certificate verify
 failed
 Failed to enable crypto
 failed to open stream: operation failed
```

## 解决方法

1.下载 http://curl.haxx.se/ca/cacert.pem

2.配置 php.ini openssl.cafile = c:\xxx\cacert.pem
