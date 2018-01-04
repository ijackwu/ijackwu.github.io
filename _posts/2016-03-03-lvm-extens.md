---
title: "LVM 扩容 - 小记"
category: "linux"
---

> 目前空间 --- 之前用的 ext4 空间12T以上就不能识别了。。。坑爹，还是上xfs格式

##  查看磁盘情况

```
[root@samba ~]# df -h
Filesystem               Size  Used Avail Use% Mounted on
/dev/sda4                265G 1004M  251G   1% /
tmpfs                     16G     0   16G   0% /dev/shm
/dev/sda2                194M   26M  158M  14% /boot
/dev/sda1                 50M  254K   50M   1% /boot/efi
/dev/mapper/camelvg-lv2   25T   15T   11T  57% /camel2   -- 待扩容
```

## lvs情况

```
[root@samba ~]# lvm
lvm> lvs
  LV   VG      Attr       LSize  Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  lv2  camelvg -wi-ao---- 24.70t    
```

> pvs 情况 都是4T 大分区，这边使用的gpt分区，mbr不能识别分区空间2T以上，可以格式化，但是浪费2T+空间

```
lvm> pvs
  PV         VG      Fmt  Attr PSize    PFree  
  /dev/sdb1  camelvg lvm2 a--  1000.00g      0 
  /dev/sdc1  camelvg lvm2 a--     4.88t 707.18g
  /dev/sdd1  camelvg lvm2 a--     4.88t   4.88t
  /dev/sde1  camelvg lvm2 a--     4.88t   4.88t
  /dev/sdf1  camelvg lvm2 a--     4.88t      0 
  /dev/sdg1  camelvg lvm2 a--     4.88t   4.88t
  /dev/sdh1  camelvg lvm2 a--     4.88t   4.88t
  /dev/sdi1  camelvg lvm2 a--     4.88t      0 
  /dev/sdj1  camelvg lvm2 a--     4.88t      0 
  /dev/sdk1  camelvg lvm2 a--     4.88t      0 

```

## vgs情况

```
lvm> vgs
  VG      #PV #LV #SN Attr   VSize  VFree 
  camelvg  10   1   0 wz--n- 44.92t 20.22t
lvm> 
```

> 目前系统 25T，用了15个T

```
[root@samba ~]# df -h
Filesystem               Size  Used Avail Use% Mounted on
/dev/sda4                265G 1003M  251G   1% /
tmpfs                     16G     0   16G   0% /dev/shm
/dev/sda2                194M   26M  158M  14% /boot
/dev/sda1                 50M  254K   50M   1% /boot/efi
/dev/mapper/camelvg-lv2   25T   15T   11T  58% /camel2
```

## 加1000G 玩下

```
[root@samba ~]# lvextend -L +1000G /dev/mapper/camelvg-lv2  control      
  Size of logical volume camelvg/lv2 changed from 24.70 TiB (6474957 extents) to 25.68 TiB (6730957 extents).
  Logical volume lv2 successfully resized
```

> 还要再执行下，xfs_growfs. 如果是ext格式的用resize2file

```
[root@samba ~]# xfs_growfs /camel2/
meta-data=/dev/mapper/camelvg-lv2 isize=256    agcount=25, agsize=268435455 blks
         =                       sectsz=512   attr=2, projid32bit=0
data     =                       bsize=4096   blocks=6630355968, imaxpct=5
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0
log      =internal               bsize=4096   blocks=521728, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
data blocks changed from 6630355968 to 6892499968
```

> 再看看空间有了么有，26T 完事。

```
[root@samba ~]# df -h
Filesystem               Size  Used Avail Use% Mounted on
/dev/sda4                265G 1003M  251G   1% /
tmpfs                     16G     0   16G   0% /dev/shm
/dev/sda2                194M   26M  158M  14% /boot
/dev/sda1                 50M  254K   50M   1% /boot/efi
/dev/mapper/camelvg-lv2   26T   15T   12T  55% /camel2
```

> 这里说下，之前各种坑爹的事情，上的存储系统，做了lvs发现空间莫名消失了，各种找原因，原来是ext3格式不支持12T以上磁盘，然后就折腾了。 建立一个新的lv，然后把老的迁移过来，高危操作，几十T数据，没完好就会打包走人，哈哈，，，小弟不是运维，坑的是运维跑路了剩下来协助这块烂摊子。

## 看下 fstab 大家就懂了

```
[root@samba ~]# cat /etc/fstab 
#
# /etc/fstab
# Created by anaconda on Tue Sep 22 13:42:02 2015
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=5cd2487b-b56e-40cf-a927-118a6e9ba566 /                       ext4    defaults        1 1
UUID=a4953598-b0e8-4915-833d-a9e4bace4d8b /boot                   ext4    defaults        1 2
UUID=9ED8-F9C4          /boot/efi               vfat    umask=0077,shortname=winnt 0 0
UUID=fa66df00-ab0a-4978-80e0-eeff2dead086 swap                    swap    defaults        0 0
tmpfs                   /dev/shm                tmpfs   defaults        0 0
devpts                  /dev/pts                devpts  gid=5,mode=620  0 0
sysfs                   /sys                    sysfs   defaults        0 0
proc                    /proc                   proc    defaults        0 0
#/dev/camelvg/lv1   /camel          ext4    defaults    0 0
/dev/camelvg/lv2    /camel2         xfs defaults    0 0
[root@samba ~]# 
```
