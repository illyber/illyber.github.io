---
title: find
categories:
  - Linux
date: 2024-04-02 05:20
tags:
  - 搜索/find
---

---


<!-- toc -->
# find
更多参见：[菜鸟教程 - Linux find 命令](https://www.runoob.com/linux/linux-comm-find.html)
## 按文件名查找 -name
‘-name’ matches against basenames only
查找当前目录下名为 file.txt 的文件：
```shell
find . -name file.txt
```

将当前目录及其子目录下所有文件后缀为 .c 的文件列出来:
```shell
find . -name "*.c"
```
## 文件类型 -type
将当前目录及其子目录中的所有文件列出：
```shell
find . -type f
```
## 按大小查找
- 查找 /home 目录下大于 1MB 的文件：
```shell
find /home -size +1M
```
## 排除指定目录 -prune
- 在 `/home/carryf` 里搜索 `"cdr_*.conf"` ,并且排除 `/home/carryf/astetc` 目录

```shell
find /home/carryf -path "/home/carryf/astetc" -prune -o -type f -name "cdr_*.conf" -print
find <src-path> -path '<ignor-path1>' -prune -o -path '<ignor-path2>' -prune -o -print
```





---
