---
title: "mysql原来desc还有exlain作用"
category: "mysql"
---

```
MariaDB [t]> desc select * from upgrades;
+------+-------------+------------+------+---------------+------+---------+------+------+-------+ | id | select_type | table | type | possible_keys | key |
key_len | ref | rows | Extra |
+------+-------------+------------+------+---------------+------+---------+------+------+-------+ | 1 | SIMPLE | upgrades | ALL | NULL | NULL | NULL
| NULL | 1 | |
+------+-------------+------------+------+---------------+------+---------+------+------+-------+ 1 row in set (0.00 sec)

MariaDB [t]> explain select * from upgrades;
+------+-------------+-------------+------+---------------+------+---------+------+------+-------+ | id | select_type | table | type | possible_keys | key |
key_len | ref | rows | Extra |
+------+-------------+-------------+------+---------------+------+---------+------+------+-------+ | 1 | SIMPLE | upgrades | ALL | NULL | NULL |
NULL | NULL | 1 | |
+------+-------------+-------------+------+---------------+------+---------+------+------+-------+ 1 row in set (0.00 sec)
```


