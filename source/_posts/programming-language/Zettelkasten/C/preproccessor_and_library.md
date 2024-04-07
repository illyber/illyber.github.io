---
title: C 预处理器和 C 库
tags:
  - C
categories:
  - Language
---
# C 预处理器

## typedef（P411）
定义新类型。
```c
typedef description name;
typedef unsigned char BYTE;
typedef void (*V_FP_CHARP)(char *); //定义了V_FP_CHARP. 被定义的标识符代替了过程。
void show (V_FP_CHARP fp, char *);
```

与struct联合应用，struct 括号里包含新类型名时，两个新类型名
```c
typedef struct bitnode{
    int data;
    struct bitnode *lchild, *rchild;
} bitnode, *bitree;
```
## \#define

\#define 可用来定义符号常量。宏（macro）的名称中不允许有空格，ANSI C允许在参数列表中使用空格。而且必须遵循C变量的命名规则：只能使用字符、数字和下划线（_）字符，而且首字符不能是数字。

![image-20221028015011129](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281527069.png)

带有参数的宏

![image-20221028130153811](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281527070.png)

```c
#define SQUARE(X) X*X
//SQUARE(x+2)⇒x+2*x+2
//100/SQUARE(2)⇒100/2*2

//所以最好多加括号
#define SQUARE(X) ((X)*(X))
```

## 井号运算符
将参数转换为字符串，利用字符串的串联特性。

```c
#define PSQR(X) printf("The square of " #X " is %d.\n", ((X)*(X)))
int y=5;
PSQR(y);
//替换后的结果是
printf("The square of ""y"" is %d.\n", ((y)*(y)));
```

## 双井号运算符
将两个标识符组合成一个。

```c
#define XNAME(n) x ## n
#define PRINT_XN(n) printf("x" #n " = %d\n", x ## n)
int XNAME(1)= 14;	//becomes int x1= 14;
PRINT_XN(1);	//becomes printf("x1 = %d\n", x1);
```

变参宏。`...`和`__VA_ARGS__`。省略号只能代替最后的宏参数。

```c
#define PR(X, ...) printf("Message " #X ": " _ _VA_ARGS_ _)
```

## #include

```c
#include <stdio.h> 			#查找系统目录
#include "hot.h" 			#查找当前工作目录
#include "/usr/biff/p.h"  	#查找/usr/biff目录
```

## 其它def预处理指令
`#undef` : 取消 `#define` 定义的宏。
`#ifdef` , `#else` , `#endif` : 条件编译。eg:
```c
#ifdef MAVIS
	#include "horse.h" // gets done if MAVIS is #defined
	#define STABLES 5
#else
	#include "cow.h"   // gets done if MAVIS isn't #defined
	#define STABLES
15
#endif
```
`#ifndef` , `#endif` : 条件编译。eg:
```c
#ifndef SIZE
#define SIZE 100
#endif
```

`#if` 和 `#elif`. 可以在指令中使用 C 的关系运算符和逻辑运算符：
```c
#if SYS == 1
#include "ibm.h"
#endif

#if SYS == 1
#include "ibmpc.h"
#elif SYS == 2
#include "vax.h"
#elif SYS == 3
#include "mac.h"
#else
#include "general.h"
#endif
```
## 预定义宏
![预定义宏](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281527071.png)

## #line

重新设置行号和文件名

## #error

输出指定的错误信息

## #pragma

把编译器指令放入源代码中

_Pragma 把字符串转换为编译指示

## `_Generic`

```c
_Generic(x, int:0, float:1, default:3)
```

## 内联函数（inline function)(C99)

1. 唯二的函数说明符之一
2. 内联函数定义必须与调用该函数的代码在一个文件
3. 如果别的文件要调用内联函数，可以把内联函数定义放在头文件，这是个例外，一般头文件不放定义。

## _Noreturn

1. 唯二的函数说明符之一
2. 调用完该函数之后，不返回主调函数

# C 库

## 历史-void指针

ANSI C 有void指针，void 指针用于指针类型不确定的情况。

## 数学库

- 数学库里三角函数的自变量是弧度
- atan()不能区分象限，atan2()能区分象限

## 通用工具库

- int atexit( void (*func)(void) )

register function. 将 `*func` 入栈，ANSI C容量是32个函数；调用exit()时执行栈内函数，后进先出；main()结束时会自动隐形调用exit()

- exit()

0: 成功，非零：失败。

或用预定义宏：EXIT_SUCCESS, EXIT_FAILURE

- qsort()。快速排序。

- `void qsort( void *base, size_t nmemb, size_t size, int (* compar)(const void *, const void *))`
  - `void *`。C语言中，任何指针都可以赋值给void指针；C++ 中必须要强制类型转换
  - base. 数组的首元素地址；
  - nmemb. number of memory by bytes. 要比较的项的数量；
  - size. 单元素的字节大小。因为用void指针，不知道数组元素大小；
  - compar. 函数指针，该函数用于比较。规定：如果第一个元素大于第二个，返回正数；相等，0；小于，负数。
    - compar 内部。要用对应的元素指针访问元素，要对`void *`变量强制类型转换。为了方便移植到C++

## The Assert Library

- assert()
  - 用 assert.h 头文件；assert() 是一个宏
  
  - assert() 里放整型表达式（关系表达式和逻辑表达式）
  
  - 用于debug。如果表达式为假，会输出错误信息帮助debug
  
  - 在 `#include<assert.h>` 前放#define NDEBUG，编译器会禁用所有assert()语句
  
  - ```c
    //在标头 <assert.h> 定义
    #ifdef NDEBUG
    #define assert(condition) ((void)0)
    #else
    #define assert(condition) /*implementation defined*/
    #endif
    ```
  
- `_Static_assert(表达式, 消息)`(C11)
  
  - 不需要include assert.h
  - 第一个参数：整型常量表达式；第二个参数：字符串。sizeof表达式被视为整型常量
  - 在编译时检查第一个参数，如果错，就显示字符串

## memcpy()和memmove()

- `void *memcpy( void * restrict  s1, const void * restrict s2, size_t n)`
- `void *memmove( void * s1, const void * s2, size_t n)`
- 两者函数原型都位于string.h
- 都是从s2复制到s1, memmove()不是移动
- memcpy()假设两块内存没有重叠

