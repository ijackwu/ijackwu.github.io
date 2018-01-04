---
title: "rsync @ERROR: auth failed on module "
category: "linux"
---

搞了一天，想死!

```
@ERROR: auth failed on module ***

read only = no#是否只读
```

正常看没有问题的，其实问题就出在备注。

安全考虑还是下面这种方式

```
#是否只读
read only = no
```


