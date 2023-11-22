---
title: 指针
tags:
  - C
categories:
  - Language
  - C
  - data_type
---
# 英语读法

- `*x` 读作: pointed by x （由x指向的）
- &x 读作: address of x（x的地址）
- x.y 读作: member y of object x （对象x的成员y）
- `(*x).y` 读作: member y of object pointed by x（由x指向的对象的成员y）
- x->y 读作: member y of object pointed by x (同上一个等价)
- x[0] 读作: first object pointed by x（由x指向的第一个对象）
- x[1] 读作: second object pointed by x（由x指向的第二个对象）
- x[n] 读作: (n+1)th object pointed by x（由x指向的第n+1个对象）
# 指针类型的意义
指针类型的不同在于移动时的单位距离不同，即 p++ 的结果不同。

# printf()格式转换符

- `%td`：十进制输出地址
- `%p`：16进制输出地址

# 指针相减

指针求差：差值的单位与数组类型的单位相同。例如，程序清单10.13的输出中，ptr2 - ptr1得2，意思是这两个指针所指向的两个元素相隔两个int，而不是2字节。只要两个指针都指向相同的数组（或者其中一个指针指向数组后面的第 1 个地址），C 都能保证相减运算有效。如果指向两个不同数组的指针进行求差运算可能会得出一个值，或者导致运行时错误。

# 指针与数组（14.13 P412）

指针本身的类型, 指针所指向的类型

()和[]的优先度比 * 高。
指针名，指针的间隔，指向的变量

```c
int (* rusks)[10]; // 声明一个指向数组的指针，该数组内含10个int类型的值
int *rusks[10];//指针数组，内含10个元素，每个元素指向int.
double (*pf[10])(double, double);//函数指针数组，10个元素
```

# 函数指针

1. 函数名是函数的地址

2. 定义函数指针

   ```c
   void (*pf)(char *);//pf指向一个返回值为void，形参为char *的函数
   double (*pf[10])(double, double);//函数指针数组，10个元素
   double (*pf[])(double, double)={ add, sub, mul, div_i};//定义并初始化指针数组
   ```

3. 引用函数指针

   ```c
   char *st;
   pf(st);
   (*pf)(st);
   //两种形式都行
   ```

# const 关键字