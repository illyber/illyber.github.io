---
title: multi-files
date: 2024-04-05 22:52
tags:
  - C
categories:
---
---
# 跨文件定义/引用结构体
## main.c文件中不能使用结构体样式
三个文件：a.h, b.c, main.c
```c file:a.h
typedef struct node node;
typedef struct node * ptrtonode;
```

```c file:b.c
//用来定义函数
struct node
{
    int coef;//系数
    int expo;//指数
    struct node *next;
};
void function(...)
```

```c file:main.c
//调用 b.c 中的函数
int main( int argc, char * argv[])
{
	//...
	return 0;
}
```

在 b.c 里可以用 node 而不是 struct node 定义变量；但是在 main.c 里不能用 struct node/node 定义变量。
在实际使用中，不会把结构体暴露出去，我们会提供函数让别人去调用，就像文件读写样，你不需要知道FILE的具体结构，而是调用系统提供的函数fread,fwrite等等。

## main.c文件中可以引用结构体样式
在 main.c 中 include b.c

在实际使用中，不会把结构体暴露出去，我们会提供函数让别人去调用，就像文件读写样，你不需要知道FILE的具体结构，而是调用系统提供的函数fread,fwrite等等。


---