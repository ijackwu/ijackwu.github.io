---
title: "数据库单例"
category : "php"
---

```php
class db 
{
   
    private static $_instance;

    private static $_db_map = [
	    'mysqli' => 'MysqliDrive',
	    'pdo' => 'PdoDrive',
    ]; 

    public static function getInstance($type = "pdo")
    {
        if (!self::$_db_map[$type]) {
            throw  new Exception('db type error!');
            die;
        }

        if (self::$_instance[$type]) {
            self::$_instance[$type] = new self::$_db_map($type);
        }

        return self::$_instance[$type];
    }
}

class MysqliDrive extends DbDrive
{
    public function connection($host, $userName, $passWord, $port = 3306){}
    public function select() {}
}

class PdoDrive extends DbDrive
{
    public function connection($host, $userName, $passWord, $port = 3306){}
    public function select() {}
}
```
