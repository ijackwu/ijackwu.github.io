---
title: "常用域名网络命令"
category: "linux"
---

## 查看A记录

```
nslookup
kdkd8.com
Server: 100.127.1.1
Address: 100.127.1.1#53

Non-authoritative answer:
kdkd8.com canonical name = jackwu.sinaapp.com.
jackwu.sinaapp.com canonical name = sinaapp.com.
Name: sinaapp.com
Address: 220.181.136.41
Name: sinaapp.com
Address: 220.181.136.30

```

## 查看dns

```
set type=ns
kdkd8.com
Server: 100.127.1.1
Address: 100.127.1.1#53

Non-authoritative answer:
kdkd8.com nameserver = f1g1ns1.dnspod.net.
kdkd8.com nameserver = f1g1ns2.dnspod.net.

Authoritative answers can be found from:
```




