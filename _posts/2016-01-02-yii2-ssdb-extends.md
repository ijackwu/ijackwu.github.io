---
title: "yii2 ssdb 扩展"
category: "php"
---

要用到SSDB，所以就简单改了，放到composer。

## Yii2-ssdb - a Yii 2.0 SSDB extension

## Requirements
Yii 2.0 or above

## Installation
The preferred way to install this extension is through composer.

```
composer require 'ijackwu/yii2-ssdb:dev-master'
```

## Configuration

To use this extension, you have to configure the Connection class in your application configuration:

```
return [
    //....
    'components' => [
        'ssdb' => [
            'class' => 'ijackwu\ssdb\Connection',
            'host' => 'localhost',
            'port' => 8888,
        ],
    ]
];
```

https://github.com/ijackwu/yii2-ssdb




