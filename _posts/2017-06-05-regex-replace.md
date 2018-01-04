---
title: "某公司正则面试题"
category: "正则"
---

## text.txt 文件内容

```html
<span>Welcome</span><b>Tester</b><span>Tiiiii</span>
```

## 替换后代码

```
<span>1@Welcome</span><b>2@Tester</b><span>3@Tiiiii</span>
```

## 代码

```php
$str = file_get_contents('./test.txt');
echo $str . "\n";
preg_match_all('!<(?:span|b)\s*[^>]*>(\s*[^>]+)</(?:span|b)>!', $str, $out);

//print_r($out);

foreach($out[0] as $key => $val) {
    $tmp_key = $key + 1;
    // 替换 xx => 1@xx
    $tmp = str_replace($out[1][$key], $tmp_key . '@' .$out[1][$key], $val);
    echo "---tmp",  $tmp, "\n";
    // 定位字符串所在位置
    $pos = strpos($str, $val );
    echo "---post",  $pos, "\n";
    // 替换
    $str = substr_replace($str, $tmp, $pos, strlen($val));
}
```

