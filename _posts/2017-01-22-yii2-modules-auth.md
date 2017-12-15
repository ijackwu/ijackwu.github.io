---
title: yii2 modules 通用登录验证配置
category: yii2
author: 酱油先生
---

```php
parent::init();
Yii::$app->errorHandler->errorAction = 'admin/default/error';
Yii::$app->admin->loginUrl = ['default/login'];
Yii::$app->homeUrl = "/admin/default/index";

// 如果登录，并且不是站点管理员，直接退出
if (!Yii::$app->admin->isGuest && Yii::$app->admin->identity->user_type != User::TYPE_ADMIN) {
	Yii::$app->admin->logout();
}
```
