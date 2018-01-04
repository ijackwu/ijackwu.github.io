---
title: "mysql varchar类型 where条件不加引号引发性能问题"
category: "mysql"
---

## 表结构

```mysql
mysql> show create table api_taobao_sku\G

*************************** 1. row ***************************
       Table: api_taobao_sku
Create Table: CREATE TABLE `api_taobao_sku` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `sd_id` int(11) NOT NULL,
  `sddm` varchar(20) DEFAULT NULL,
  `item_id` int(11) NOT NULL,
  `properties_name` varchar(255) DEFAULT NULL,
  `sku_id` varchar(30) NOT NULL,
  `iid` varchar(255) DEFAULT NULL,
  `num_iid` varchar(255) DEFAULT NULL,
  `properties` varchar(255) DEFAULT NULL,
  `quantity` int(11) DEFAULT NULL,
  `price` varchar(255) DEFAULT NULL,
  `outer_id` varchar(255) DEFAULT NULL,
  `created` varchar(255) DEFAULT NULL,
  `modified` varchar(255) DEFAULT NULL,
  `status` varchar(255) DEFAULT NULL,
  `sku` varchar(255) DEFAULT NULL,
  `goods_id` varchar(255) DEFAULT NULL,
  `goods_sn` varchar(255) DEFAULT NULL,
  `color_id` varchar(255) DEFAULT NULL,
  `color_name` varchar(255) DEFAULT NULL,
  `Size_id` varchar(255) DEFAULT NULL,
  `Size_name` varchar(255) DEFAULT NULL,
  `is_sale` tinyint(3) DEFAULT '0',
  `is_relation` tinyint(3) DEFAULT '0',
  `is_del` tinyint(3) DEFAULT '0',
  `is_synckc` tinyint(3) DEFAULT '0',
  `is_wlb` tinyint(3) DEFAULT '0',
  `updated` datetime DEFAULT NULL,
  `is_update` tinyint(3) DEFAULT '1' COMMENT '??????????????????????????',
  `sale_mode` varchar(20) NOT NULL COMMENT '???????stock???presale',
  `delivery_mode` varchar(20) NOT NULL DEFAULT 'days' COMMENT 'days?????? ; time??????',
  `delivery_days_or_time` varchar(20) NOT NULL COMMENT '??????????????',
  `chayi` tinyint(2) NOT NULL DEFAULT '0' COMMENT 'sku????,0???1??',
  `ck_diff` int(11) DEFAULT NULL COMMENT '??null,1????',
  `is_huodong` tinyint(4) DEFAULT '0',
  `prop_name_error` tinyint(2) NOT NULL DEFAULT '0' COMMENT '0->??,1???????2????3goods_barcode????sku,4api_taobao_sku??????,5goods_color,goods_size???????',
  PRIMARY KEY (`id`),
  UNIQUE KEY `sku_id` (`sku_id`),
  KEY `id_item_id` (`item_id`),
  KEY `num_iid` (`num_iid`),
  KEY `outer_id` (`outer_id`),
  KEY `nii_index` (`num_iid`,`is_del`,`is_wlb`)
) ENGINE=InnoDB AUTO_INCREMENT=2233175693 DEFAULT CHARSET=utf8
1 row in set (0.00 sec)
```

## 不加引号 -- 全表扫描

```mysql
mysql> explain select * from efast.api_taobao_sku where num_iid =39065521213 and is_del=0 and is_wlb=0;
+----+-------------+----------------+------+-------------------+------+---------+------+---------+-------------+
| id | select_type | table          | type | possible_keys     | key  | key_len | ref  | rows    | Extra       |
+----+-------------+----------------+------+-------------------+------+---------+------+---------+-------------+
|  1 | SIMPLE      | api_taobao_sku | ALL  | num_iid,nii_index | NULL | NULL    | NULL | 1496125 | Using where |
+----+-------------+----------------+------+-------------------+------+---------+------+---------+-------------+
1 row in set (0.00 sec)
```

## 加引号 -- 常量级别

```mysql
mysql> explain select * from efast.api_taobao_sku where num_iid ='39065521213' and is_del=0 and is_wlb=0;
+----+-------------+----------------+------+-------------------+---------+---------+-------+------+-------------+
| id | select_type | table          | type | possible_keys     | key     | key_len | ref   | rows | Extra       |
+----+-------------+----------------+------+-------------------+---------+---------+-------+------+-------------+
|  1 | SIMPLE      | api_taobao_sku | ref  | num_iid,nii_index | num_iid | 768     | const |   14 | Using where |
+----+-------------+----------------+------+-------------------+---------+---------+-------+------+-------------+
1 row in set (0.00 sec)
```

