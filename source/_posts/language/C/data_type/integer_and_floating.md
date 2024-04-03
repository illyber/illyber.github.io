---
title: 整型和浮点
tags:
  - C
categories:
  - Language
---
## 大小一览
linux 上的大小。
一字节的定义是char类型的大小

|              | char | short | int   | long   | long long   |
| ------------ | ---- | ----- | ----- | ------ | ----------- |
| 字节（byte） | 1    | 2     | 4     | 8      | 8           |
|              |      |       | float | double | long double |
| 字节（byte） |      |       | 4     | 8      | 16          |

## 整型

### 常量

0开头是八进制，0x开头是16进制。

### `_Bool`类型

_Bool 的大小由编译器决定；

stdbool.h 头文件 定义 bool 为 _Bool 的别名，定义了值为1和0的符号变量true, false.

### size_t (size type)

size_t 的大小由具体的计算机决定，方便移植；

debian/ASUS u4000u 的大小为 8 字节；SIZE_MAX 是 size_t 的最大值，当前定义在 stdint.h

### time_t

time_t 格式转换符是

善用 const 关键字

## 浮点型

在K&R C中，表达式或参数中的float类型值会被自动转换成double类型。


