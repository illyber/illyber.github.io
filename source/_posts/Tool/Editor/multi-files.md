---
title: vim多文件操作
tags:
  - vim
categories:
  - Tool
  - Editor
---

# 相关概念

- `:n`. 打开新文件

window, tab, buffer 的区别
![difference](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307011639644.png)

# 窗口

## 以多窗口打开文件
`-O` 分屏打开文件。大写左右分屏，小写上下分屏。eg:
```shell
vim -o file1 file2
```


## 打开新文件的ex命令

在进入Vim后，可以使用这些命令来打开/关闭窗口：

```vimscript
:vs[plit] {file}    垂直分屏

:new {file}         水平分屏
:sp[lit] {file}     水平分屏
:sv[iew] {file}     水平分屏，以只读方式打开

:clo[se]            关闭当前窗口
```

## 切换窗口

切换窗口的快捷键就是`Ctrl+w`前缀 + `hjkl`：

```vimscript
Ctrl+w w        遍历切换窗口
Ctrl+w h        切换到左边窗口
Ctrl+w j        切换到下边窗口
Ctrl+w k        切换到上边窗口
Ctrl+w l        切换到右边窗口
```

> 还有`t`切换到最上方的窗口，`b`切换到最下方的窗口。

## 开关窗口的快捷键

上述命令都有相应的快捷键，它们有共同的修饰键：`Ctrl+w`。

```vimscript
Ctrl+w q        关闭当前窗口
Ctrl+w s        水平分割当前窗口
Ctrl+w v        垂直分割当前窗口
Ctrl+w n        打开一个新窗口（空文件）
Ctrl+w o        关闭出当前窗口之外的所有窗口
Ctrl+w T        当前窗口移动到新标签页
```

## 调整窗口大小

调整窗口大小的快捷键仍然有`Ctrl+W`前缀：

```
Ctrl+w +        增加窗口高度
Ctrl+w -        减小窗口高度
Ctrl+w =        统一窗口高度
```

## 移动窗口

分屏后还可以把当前窗口向任何方向移动，只需要将上述快捷键中的`hjkl`大写：

```
Ctrl+w H        向左移动当前窗口
Ctrl+w J        向下移动当前窗口
Ctrl+w K        向上移动当前窗口
Ctrl+w L        向右移动当前窗口
```

# tab（标签页）

[vim多文件编辑：标签页](https://harttle.land/2015/11/12/vim-tabpage.html)

使用`-p`参数来用多个标签页启动Vim：

```vimscript
vim -p main.cpp my-oj-toolkit.h /private/etc/hosts
```

在新标签页打开文件

```vimscript
:tabe[dit] filename
```

切换标签页

```vimscript
gt
gT
[number]gt
```

# buffer