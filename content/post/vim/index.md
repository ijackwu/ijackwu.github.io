---
title: "Vim学习记录"
description: 
date: 2024-05-05T16:44:00+08:00
image: 
math: 
license: 
hidden: false
comments: true
draft: true
---

## 插入模式编辑指令

从`insert -> normal` ESC,也可以用`ctrl+[` 或者 `ctrl+c`

普通模式下:

小写

`a` append 光标后插入

`i` before 光标前插入

`o` open a new line 下一行插入

大写(记忆方法`a`是后面插入大写`A`就是行末，`i`是光标前面插入，大写I就是行首，`o`是下一行，大写`O`相反上一行插入)

`A` append after line 行末插入

`I` append before line 行首插入

`O` append a line above 上一行插入


编辑操作

`ctrl+h` 撤销光标前面上一个字符

`ctrl+w` 撤销光标前面一个单词

`ctrl+u` 撤销一行

`gi` 快速回到上一次编辑的位置

## 分屏

`:sp` 横分屏

`:vs` 竖分屏

## 视图模式

`v` 选中

`V` 行选中

`ctrl + v` 列选中

## 视图模式下移动光标

```shell
    k
h       l
    j
```

## 单词移动

`w`, `e` 下一个单词首（尾）、非空白字符分割单词

`W`, `E` 下一个单词首(尾)、空白字符分割单词

`b` 上一个单词首

`B` 上一个单词尾

## 行内查找

`f` 查找内容,`;`重复一次查找下一个，`,`相反方向查找
`F`逻辑和`f`相反，反向查找

`t`和`f`一样，只是搜索到内容光标定位到搜索的前一个字符

## 行内移动

`^`和`0`移动行首

`$`和`g_`移动行尾

## 文件跳转

`gg` 第一行

`G` 最后一行

`ctrl+o` 返回上一个位置

`ctrl+]` 进入 一个函数定义

## 文件状态

`ctrl+g` 查看文件状态

`行数+G`, `:行数` 跳到文件行数字

## vim中执行系统命令

`:!命令` 例如执行系统`ls`, `:!ls`

有一个场景比较方便修改文件切换权限，比如编辑`/etc/hosts`，普通用户模式下只读打开，需要修改保持的时候没权限，可以这样操作。

`:w !sudo tee %`

## 屏幕移动

`ctrl+u` upword 向上翻页

`ctrl+f` forward 向下翻页

`zz` 光标内容移动到屏幕中间

`H` head 顶部

`M` middler 光标跳到中间

`L` lower 底部
