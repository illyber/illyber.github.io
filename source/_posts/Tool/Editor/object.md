---
title: Vim Object
tags:
  - vim
categories:
  - Tool
  - Editor
---
![image-20230115202343272](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281946922.png)
- 基础类型：
  - word (w)
  - sentence (s)
  - paragraph (p)
- 高阶 Surround 类型：
  - `[], "", ' ', ``, {}, ()`
- 高阶 Tag 类型（t）
- 选中类型：
  - 不包括空格   inner (i)
  - 包括尾部空格 around (a)

operator 和 object 一起使用：operator{object}

- `diw` 光标在中间时也可以删除整个单词，不删除后面的空格
- `daw` 光标在中间时也可以删除整个单词，删除后面的空格