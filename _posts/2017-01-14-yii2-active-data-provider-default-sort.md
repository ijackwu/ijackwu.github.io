---
title: yii2 ActiveDataProvider 默认排序配置
category: yii2
author: 酱油先生
---

```php
$dataProvider = new ActiveDataProvider([
    'query' => $query,
    'sort' => [
        'defaultOrder' => [
            'id' => SORT_DESC,  // 需要排序字段 => 排序类型 [SORT_DESC, SORT_ASC]          
        ]
    ],
]);

```
