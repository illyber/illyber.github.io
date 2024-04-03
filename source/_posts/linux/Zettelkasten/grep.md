---
title: grep
date: 2024-04-02 03:07
tags:
  - 文本处理/grep
categories:
  - Linux
aliases: 
time: '2024-04-02 03:07'
---

```bash
grep pattern filelist
```
grep 会输出符合模式的文件名

-i 忽略大小写
-w 匹配整个单词
-e 查找多个字符串。grep -e pattern 1 -e pattern 2 file
-n 打印目标的行数
-v 打印不符合模式的行
-r 递归查找文件，用于目录
-l 打印包含模式的文件名
-E, --extended-regexp 启用扩展正则表达式

搜索不出结果的时候，可以试试 -e 选项