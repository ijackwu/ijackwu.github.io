---
title: "css巧妙设计"
category: "css"
---

使用遮罩修改图标

```html
<form enctype="multipart/form-data" action="" method="post" class="form"> <input type="file" style="position:absolute;height: 28px;top:0;width: 100%;right: 0px;filter:alpha(opacity=0);opacity:0;z-index: 2;" name="file" onchange="$('#sztp').click();" id="imgsrc"> <input style="padding:0;margin:0;border:1px solid
#dcdcdc;background:#f1f1f1;width:82px;height:28px;float:left;margin-left:5px;text-align:center;line-height:28px;position: absolute;" value="上传文件"> <input type="hidden" value="upaccess1" name="name"> <input type="submit" style="display:none;" id="sztp"> </form>
```

