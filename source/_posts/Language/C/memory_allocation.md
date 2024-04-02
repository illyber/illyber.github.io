---
title: 内存分配
tags:
  - C
categories:
  - Language
---
# malloc(), exit(), free()

| 函数                        | 作用                         | 参数                                               | 返回值                                                       |
| --------------------------- | ---------------------------- | -------------------------------------------------- | ------------------------------------------------------------ |
| `void *malloc( size_t size )` | 分配 size 字节的内存         | size_t                                             | 以 void* 格式，返回内存的首字节地址                          |
| `void exit( int exit_code )`  | 结束程序                     | int 类型的 exit_code, (EXIT_SUCCESS, EXIT_FAILURE) | exit_code 为EXIT_SUCCESS(即0) ，返回指示成功终止的实现定义状态。<br />exit_code 为 EXIT_FAILURE(即1)，则返回指示不成功终止的实现定义状态。<br />其他情况下返回实现定义的状态值。 |
| `void free( void *ptr )`      | 释放malloc(), calloc()的内存 |                                                    |                                                              |

## malloc 的使用

虽然 malloc() 的 void * 相当于通用指针，但是还是建议用 `(double *)` 这样的强制类型转换，便于阅读和转换为 C++ 程序。

```c
int n;
double *ptr;
ptr = (double *) malloc(n*sizeof(double));
```

## exit()

EXIT_SUCCESS 是 0，定义在 stdlib.h；EXIT_FAILURE 是 1，定义在 stdlib.h。

# calloc() 函数

建议使用强制类型转换和 sizeof() ，方便移植；

```c
void *calloc( size_t num, size_t size);  //函数原型
```

calloc() 按单元数量分配内存，并把所有位设为 0；num 是单元数量，size 是一个单元的字节数；由 free() 释放内存。
# 静态内存分配
指在编译时分配内存
# 动态内存分配和变长数组

# 存储类别和动态内存分配

同一存储类别存储在一起；静态数据（包括字符串变量）存储在一个区域，自动数据存储在一个区域，动态数据存储在一个区域（内存堆/自由内存）。

# memcpy()和memmove()

- `void *memcpy( void * restrict  s1, const void * restrict s2, size_t n)`
- `void *memmove( void * s1, const void * s2, size_t n)`
- 两者函数原型都位于string.h
- 都是从s2复制到s1, memmove()不是移动
- memcpy()假设两块内存没有重叠