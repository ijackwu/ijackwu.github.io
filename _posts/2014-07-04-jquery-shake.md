---
title: "jquery js div 抖动 效果"
category: "jquery"
---

## html 代码

```html
<div id="shake">
  <img src="shake.jpg" alt="shake" /> 
</div>
```

## 下面是js

```
function shake() {
    //100为震动间隔,3为震动次数
    $('#shake').effect('shake', { times: 3 }, 100);
}
jQuery(document).ready(function() {
    setInterval("shake()", 3000);
});
```

