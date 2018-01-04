---
title: "yii2 怎么用swiftMailer发邮件？"
category: "php"
---

配置文件修改下：

```php
 'components' => [
            'mailer' => [
            'class' => 'yii\swiftmailer\Mailer',
            'viewPath' => '@common/mail',
            'transport' => [
                'class' => 'Swift_SmtpTransport',
                'host' => 'xxx',
                'username' => 'xxx',
                'password' => 'xxx',
                'port' => '465',
                'encryption' => 'tls',
            ],
            'useFileTransport' => false,// 这里true表示存储成文件不会发送，fasle才行，定义在 yii\mail\BaseMailer
        ],
```
