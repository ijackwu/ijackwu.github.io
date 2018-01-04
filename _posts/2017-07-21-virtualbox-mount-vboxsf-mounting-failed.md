---
title: VirtualBox: mount.vboxsf: mounting failed with the error: No such device centos
category: linux
---

### 解决方法

1. 添加centos 共享目录

```
VirtualBox: mount.vboxsf: mounting failed with the error: No such device

```

2. 执行

```
cd /opt/VBoxGuestAdditions-*/init  
sudo ./vboxadd setup
```

3. 错误 Building the OpenGL support module [FAILED]
```
[root@localhost init]# ./vboxadd setup Removing existing VirtualBox
non-DKMS kernel modules [ OK ] Building the VirtualBox Guest
Additions kernel modules Building the main Guest Additions module
[ OK ] Building the shared folder support module [
OK ] Building the OpenGL support module
[FAILED] (Look at /var/log/vboxadd-install.log to find out what went
wrong. The module is not built but the others are.) Doing non-kernel
setup of the Guest Additions [ OK ] Starting the
VirtualBox Guest Additions [ OK ]
```

4. 解决
```
su -
export MAKE='/usr/bin/gmake -i'
cd /opt/VBoxGuestAdditions-*/init  
sudo ./vboxadd setup
```


