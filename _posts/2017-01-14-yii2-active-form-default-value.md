---
title: yii2 ActiveForm dropDownList默认值选着项和 placeholder设置
category: yii2
author: 酱油先生
---

dorpDownList 设置默认选项
```php
$form->field($searchmodel, 'type')->dropDownList($arr, ['prompt' => '请选择')])
```

placeholder设置
```php
$form->field($searchmodel, 'startdate')->widget(DatePicker::className(),['clientOptions' => ['dateFormat' => 'yy-mm-dd']])->textInput(['placeholder' => Yii::t('app', 'Start time')])
```




