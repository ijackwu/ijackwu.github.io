---
title: "github访问慢，资源无法下载简单解决方案"
slug: "github-accsee-slow"
description: github访问慢，资源无法下载简单解决方案 
date: 2024-05-03T21:45:01+08:00
categories:
    - github
tags:
    - github
    - gitHub520
draft: false
---

解决 **raw.githubusercontent.com** 无法访问的问题

亲测好用 [github520](https://github.com/521xueweihan/GitHub520) 直接一条命令,解决问题

## linux系统

```bash
sudo sh -c 'sed -i "/# GitHub520 Host Start/Q" /etc/hosts && curl https://raw.hellogithub.com/hosts >> /etc/hosts'
```

## mac系统

```bash
sudo sed -i "" "/# GitHub520 Host Start/,/# Github520 Host End/d" /etc/hosts && curl https://raw.hellogithub.com/hosts | sudo tee -a /etc/hosts
```
