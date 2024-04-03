---
title: 编译过程
tags:
  - C
categories:
  - Language
---
# gcc带颜色

```shell
#在.bashrc里设置
#colored GCC warnings and errors
export GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'
```

# 编译过程
- 编译 include 了 math.h 的头文件时，要加 -lm 选项，即：`gcc -o 15_atoi 15_atoi.c -lm`
- `-c`	Compile and assemble, but do not link.
- `-E` preprocess
- `-S` compile
- `-c` assemble

![](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307121909804.svg)

# 编译多个文件
## 头文件里的数据结构
防止头文件里的数据结构重复定义
```c
#ifndef _headername
#define _headname 1
...
#endif
```
编译时不用指定头文件，因为已经 include 过了。
## 防止函数文件里的函数重复定义
- 若 include 了函数文件，编译时不能指定函数文件
- 若要编译时指定函数文件，则不能 include 函数文件

否则会重复定义。

