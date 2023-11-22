---
title: 随机数和时间
tags:
  - C
categories:
  - Language
  - C
---
# 随机数

[伪随机数生成](https://zh.cppreference.com/w/c/numeric/random)

步骤：获取时间->播种->生成随机数
```c
srand(time(0));
rand();

//生成 [0,N-1] 区间的随机数
rand()%N
```

只需播种一次就可以生成多个随机数。
```c
# 函数原型都在stdlib.h

void srand( unsigned seed );
# 设定 seed 种子
# 若在任何 srand() 的调用前使用 rand() ，则 rand() 表现为如同它被以 srand(1) 播种。
# 标准实践是以 time(0) 为种子。然而 time() 返回 time_t 值，而不保证 time_t 是整数类型。尽管实践中，主流实现都定义 time_t 为整数类型，且此亦为 POSIX 所要求。

int rand();
# 返回 0 与 RAND_MAX（常常是INT_MAX） 间的随机整数值（包含 0 与 RAND_MAX ）。
```

# time.h 时间

[C 语言日期和时间工具](https://zh.cppreference.com/w/c/chrono)
- epoch/unix 时间戳
从 1970 年 1 月 1 日 00:00 UTC 到当前的秒数。UTC (coordinated universal time) 非常接近于 0 时区时间。

- shell 获取 unix时间戳
`date +%s`
%s   seconds since the Epoch (1970-01-01 00:00 UTC)

- `time_t time( time_t *arg )`
返回编码成 time_t 对象的 unix 时间戳，并将其存储于 arg 指向的 time_t 对象（除非 arg 为空指针）。

- `time_t`
足以表示时间的算术 (C11 前)实数 (C11 起)类型。

- `clock_t clock(void)`
返回从关联到进程开始执行的实现定义时期的起，进程所用的粗略处理器时间。将此值除以 [CLOCKS_PER_SEC](https://zh.cppreference.com/w/c/chrono/CLOCKS_PER_SEC) 可转换为秒。只有两次对 `clock` 不同调用的返回值的差是有意义的，

- clock_t
足以表示进程所用的处理器时间的算术 (C11 前)实数 (C11 起)类型。它拥有实现定义的范围和精度。
