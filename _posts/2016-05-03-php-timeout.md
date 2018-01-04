---
title : "windows nginx php upstream timed out (10060:"
category: "php"
---

## nginx 错误日志

```
2016/05/03 09:57:55 [error] 7748#14664: *1 upstream timed out (10060: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond) while reading response header from upstream, client: 127.0.0.1, server: dev.test.com, request: "GET /t2.php HTTP/1.1", upstream: "fastcgi://127.0.0.1:9000", host: "dev.test.com"
2016/05/03 09:57:55 [error] 7748#14664: *11 upstream timed out (10060: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond) while reading response header from upstream, client: 127.0.0.1, server: dev.test.com, request: "POST /t3.php HTTP/1.1", upstream: "fastcgi://127.0.0.1:9000", host: "dev.test.com"
```

## 问题重现

```
curl 请求 http://dev.test.com/t2.php
t2.php POST 请求 http://dev.test.com/t3.php
```

## 解决方案

启用多用php-cgi利用nginx做负载负载均衡
nginx 配置如下

```
http {

        #php 5.3
        upstream fastcgi53 {  
            server 127.0.0.1:9000 weight=1;  
            server 127.0.0.1:9001 weight=1;  
            server 127.0.0.1:9002 weight=1; 
            server 127.0.0.1:9003 weight=1;   
            server 127.0.0.1:9004 weight=1;   
        }

        #php5.4
        upstream fastcgi54 {  
            server 127.0.0.1:9010 weight=1;  
            server 127.0.0.1:9011 weight=1;  
            server 127.0.0.1:9012 weight=1; 
            server 127.0.0.1:9013 weight=1; 
            server 127.0.0.1:9014 weight=1;     
        }

        server {

          upstream fastcgi53 {  
            server 127.0.0.1:9000 weight=1;  
            server 127.0.0.1:9001 weight=1;  
            server 127.0.0.1:9002 weight=1; 
            server 127.0.0.1:9003 weight=1;         
          }  

          ....
          location ~ \.php$ {
                    root           "E:/code/test";
                    fastcgi_pass   fastcgi53;
                    fastcgi_index  index.php;
                    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
                    include        fastcgi_params;

         }

       }

   } 
```

## php 启动脚本

```
echo Starting PHP5.3 FastCGI...
RunHiddenConsole.exe E:\workspace\bat\php\php-cgi.exe -b 127.0.0.1:9000 -c E:\workspace\bat\php\php.ini
RunHiddenConsole.exe E:\workspace\bat\php\php-cgi.exe -b 127.0.0.1:9001 -c E:\workspace\bat\php\php.ini
RunHiddenConsole.exe E:\workspace\bat\php\php-cgi.exe -b 127.0.0.1:9002 -c E:\workspace\bat\php\php.ini
RunHiddenConsole.exe E:\workspace\bat\php\php-cgi.exe -b 127.0.0.1:9003 -c E:\workspace\bat\php\php.ini
RunHiddenConsole.exe E:\workspace\bat\php\php-cgi.exe -b 127.0.0.1:9004 -c E:\workspace\bat\php\php.ini
```


