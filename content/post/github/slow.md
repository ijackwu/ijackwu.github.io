---
title: "github访问慢，资源无法下载简单解决方案"
slug: "github-accsee-slow"
description: 
date: 2024-05-03T21:45:01+08:00
image: 
math: 
license: 
hidden: false
comments: true
draft: false
---

 解决 raw.githubusercontent.com 无法访问的问题

`github520`亲测好用

<https://github.com/521xueweihan/GitHub520>

linux 直接一条命令:

```bash
sudo sh -c 'sed -i "/# GitHub520 Host Start/Q" /etc/hosts && curl https://raw.hellogithub.com/hosts >> /etc/hosts'
```

 mac系统

```bash
sudo sed -i "" "/# GitHub520 Host Start/,/# Github520 Host End/d" /etc/hosts && curl https://raw.hellogithub.com/hosts | sudo tee -a /etc/hosts

```
