---
title: "window Powershell 运行mysqldump导出数据乱码 --坑"
categroy: "其他"
---

通过mysqldump出来的数据，居然提示。。。百思不得其解，查找资料，原来是 powershell这鬼导致的，重新进cmd导出数据再导入

```
G:\mysql\bin>mysql -h192.168.17.200 -uroot -p < sync.sql
Enter password: ******
ERROR: ASCII '\0' appeared in the statement, but this is not allowed unless opti
on --binary-mode is enabled and mysql is run in non-interactive mode. Set --bina
ry-mode to 1 if ASCII '\0' is expected. Query: '?'.
```
