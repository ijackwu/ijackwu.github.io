---
title: 'mysql学习记录01'
# description: mysql学习笔记，字符集
date: 2024-04-28T10:35:41+08:00
draft: false
categories:
    - mysql
tags:
    - mysql
    - mysql字符集
---

## mysql字符集

### mysql字符比较集合后缀命名含义

Collation Suffix Meanings

|    Suffix    |     Meaning   |     Descript |
|:---------:| :---------------------------:  | :--------------: |
|_ai |Accent-insensitive | 不区分重音 |
|_as |Accent-sensitive | 区分重音 |
|_ci |Case-insensitive | 不区分大小写 |
|_cs |Case-sensitive | 区分大小写|
|_bin |Binary | 二进制比较 |

### mysql字符集几个级别

- 服务器
- 数据库
- 表
- 字段

如果本级别没有设置，默认继承上一层级别。


### mysql字符集涉及地方真多

```sql
mysql> show variables like 'character_set_%';
+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | utf8mb4                    |
| character_set_connection | utf8mb4                    |
| character_set_database   | utf8mb4                    |
| character_set_filesystem | binary                     |
| character_set_results    | utf8mb4                    |
| character_set_server     | utf8mb4                    |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+
```

写**php**的时候以前经常执行一句**sql**语句 `set names utf8`,
一直没有去深究过哈，只记得是乱码的时候用

以下几句的简写：

```sql
set character_set_client = utf8; 
set character_set_connection = utf8;
set character_set_results = utf8;
```

## 查看支持存储引擎

```sql
mysql> show engines;
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| Engine             | Support | Comment                                                        | Transactions | XA   | Savepoints |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| InnoDB             | DEFAULT | Supports transactions, row-level locking, and foreign keys     | YES          | YES  | YES        |
| MRG_MYISAM         | YES     | Collection of identical MyISAM tables                          | NO           | NO   | NO         |
| MEMORY             | YES     | Hash based, stored in memory, useful for temporary tables      | NO           | NO   | NO         |
| BLACKHOLE          | YES     | /dev/null storage engine (anything you write to it disappears) | NO           | NO   | NO         |
| MyISAM             | YES     | MyISAM storage engine                                          | NO           | NO   | NO         |
| CSV                | YES     | CSV storage engine                                             | NO           | NO   | NO         |
| ARCHIVE            | YES     | Archive storage engine                                         | NO           | NO   | NO         |
| PERFORMANCE_SCHEMA | YES     | Performance Schema                                             | NO           | NO   | NO         |
| FEDERATED          | NO      | Federated MySQL storage engine                                 | NULL         | NULL | NULL       |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
9 rows in set (0.00 sec)
```

### 查看UNIX域套字节socket文件

```mysql
mysql> show variables like 'socket';
+---------------+-----------------------------+
| Variable_name | Value                       |
+---------------+-----------------------------+
| socket        | /var/run/mysqld/mysqld.sock |
+---------------+-----------------------------+
1 row in set (0.18 sec)
```
