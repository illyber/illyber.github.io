---
title: 字符串
tags:
  - C
categories:
  - Language
---
# 字符串/字符数组
字符串常量也存储在某个地方。"hello" 也代表字符串的地址。

# 字符串函数

## 字符串列表

strtol()函数

```c
size_t strlen (const char *str);
//参数为地址，返回字符串长度
//返回字符串的长度，不包括空字符

strcat( char *target, const *source);
strncat( char *dest, const *source, int *n);
//string concatenation，拼接字符串
//n dest的可用空间；
//参数为两个字符串地址，返回前一个字符串地址。

strcmp( char *, char *);
//返回值：前减后决定正负
//strcmp("A", "A") is 0
//strcmp("A", "B") is -1
//strcmp("B", "A") is 1
//strcmp("C", "A") is 1
//strcmp("Z", "a") is -1
//strcmp("apples", "apple") is 1
strncmp( char *arg1, char *arg2, int n);
//比较字符串的前 n 个字符

char *strcpy( char *restrict target, const char *restrict source );
char *strncpy( char *restrict target, const char *restrict source, size_t count );
//n 是要拷贝的字符数，strncpy() 不会自动加空字符。想想为什么不加空字符？

char *strchr(const char * s, int c);
//如果s字符串中包含c字符，该函数返回指向s字符串首位置的指针（末尾的空字符也是字符串的一部分，所以在查找范围内）；
//如果在字符串s中未找到c字符，该函数则返回空指针。

char *strstr(const char * s1, const char * s2);
//该函数返回指向 s1 字符串中 s2 字符串出现的首位置。如果在 s1 中没有找到 s2，则返回空指针。
    
sprintf( char * target, 格式化字符串, source);
//数字转化为字符串：sprintf( char *target, "%d", num)
//sprintf 类似输出重定向，输出目标从屏幕改成 buffer
```

## 把字符串转换为数字 P313

| 函数原型位于stdlib.h                                         |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `atoi( char *);`                                             | 以字符串地址为参数，到'\\0'或非数字字符时停止；<br />返回数字字符串对应的 int. 即把 "100" 转换成 100，只有非数字字符时转换成0. 肯定是字符串啊，2 位及以上数会是字符串。 |
| atof(); atol();                                              |                                                              |
| strtol(const char * restrict nptr, char ** restrict endptr, int base) | nptr 是待转换的字符串的地址，endptr 指向结束位置后一个的地址，base 是写入的地址。函数返回 long |
| strtoul()                                                    |                                                              |
| strtod()                                                     | 只转换成十进制，所以只要两个参数                             |

## [数字转字符串](https://www.runoob.com/w3cnote/c-int2str.html)
sprintf();