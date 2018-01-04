---
title:mogodb安装错误 We suggest setting it to 'never'
category: linux
---

* 错误提示

```
root@yii2:/var/lib/mongodb# mongo
MongoDB shell version: 3.2.8
connecting to: test
Server has startup warnings:
2016-07-21T13:44:20.667+0800 I CONTROL  [initandlisten]
2016-07-21T13:44:20.667+0800 I CONTROL  [initandlisten] ** WARNING: /sys/kernel/mm/transparent_hugepage/enabled is 'always'.
2016-07-21T13:44:20.667+0800 I CONTROL  [initandlisten] **        We suggest setting it to 'never'
2016-07-21T13:44:20.667+0800 I CONTROL  [initandlisten]
2016-07-21T13:44:20.667+0800 I CONTROL  [initandlisten] ** WARNING: /sys/kernel/mm/transparent_hugepage/defrag is 'always'.
2016-07-21T13:44:20.667+0800 I CONTROL  [initandlisten] **        We suggest setting it to 'never'
2016-07-21T13:44:20.667+0800 I CONTROL  [initandlisten]
```

* 解决

```
echo never >>  /sys/kernel/mm/transparent_hugepage/enabled
echo never >>  /sys/kernel/mm/transparent_hugepage/defrag

```
