---
title: '(gnome-ssh-askpass:13543): Gtk-WARNING **: cannot open display:r'
category: linux
author: 酱油先生
---


ssh 一直提示错误,折腾几个小时

```
(gnome-ssh-askpass:23149): Gtk-WARNING **: cannot open display:

While git clone ***.git if get the above error.

run
```

解决方法
```
$ unset SSH_ASKPASS
```


