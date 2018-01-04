---
title: xdebug 跟踪php慢
category: php
---

### 问题

网站间接性的慢，我就推荐他用 xdebug 跟踪下看时间耗在那里

### 找问题点

* 安装 xdebug

配置`xdebug` - `php.ini` 文件
```
[xdebug]
zend_extension=/usr/lib64/php/modules/xdebug.so
xdebug.profiler_enable = on
xdebug.trace_output_dir="/tmp/xdebug"
xdebug.profiler_output_dir="/tmp/xdebug"
xdebug.profiler_output_name = cachegrind.out.%t.%p
```

* 查看日志

这个web工具不错，直接能用 https://github.com/jokkedk/webgrind


