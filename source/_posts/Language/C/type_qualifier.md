---
title: ANSI C 类型限定符
tags:
  - C
categories:
  - Language
---
# 总览

类型 (type)、存储类别 (storage class)、类型限定符 (type qualifiers)

C90 新增：const (恒常性 constancy)，volatile (易变性 volatility)；

C99 新增：restrict；

C11 新增：_Atomic，可选库 stdatomic.h，幂等的 (idempotent)；

幂等的，可以一条声明多次使用同一个限定符，多余的限定符会被忽略。

# const type qualifiers

const 关键字声明的变量，只能在初始化时设定值，后续不能赋值或递增、递减来改变变量的值。

## 1. 在指针声明和形参声明中使用 const

```c
const int *p1;
int const *p2;
int *const p3;
const int *const p4;
```

p1 和 p2 是指向 const int 的指针，const 修饰 int，p1 和 p2 能够改变指向，但不能改变指向的对象的值；

p3 是指向 int 的 const 指针，const 修饰 p3，p3 不能改变指向，但能够改变指向的对象的值；

p4 是指向 const int 的 const 指针；

总之，当 const 放在 \* 左边，不能改变指针指向对象的值；当 const 放在 \* 右边，指针不能指向别处。

```c
void display( const int array[], int limit);
```

## 2. 对全局数据使用 const

两种方法：

1. 在一个文件使用定义式声明，其他文件中使用引用式声明 (用 extern)；

2. 使用**内部链接**的全局变量时（外部链接会冲突），在头文件中定义全局变量，在其他文件中包含该头文件，就可自动定义；

   ```c
   //constant.h
   static const double PI = 3.14159;
   //file1.c
   #include "constant.h"
   //file2.c
   #include "constant.h"
   ```

# volatile type qualifiers

volatile 表示代理可以改变该变量的值；

告知编译器，编译器可针对优化。

# restrict type qualifiers

只能用于指针声明，表示只能通过该指针访问声明的对象；

告知编译器，编译器可针对优化。

# _Atomic type qualifiers

多线程编程时使用。当一个线程对一个原子类型的对象执行原子操作时，其他线程不能访问该对象。

# 旧关键字的新位置

C99 新增

```c
void ofmouth(int al[const], int a2[restrict], int n);
```

新的 static 用法，告诉编译器如何使用形式参数。

```c
double stick(double ar[static 20]);
```

