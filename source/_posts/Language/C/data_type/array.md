---
title: 数组
tags:
  - C
categories:
  - Language
---
# malloc()创建数组
# 初始化
## 整型数组初始化

未被初始化的数组元素置为0

```c
// 传统的语法
int arr[10] = {0};//所有初始化为0
int arr[6] = {0,0,0,0,0,212};//数值数组

//指定初始化器
int arr[6] = {[5] = 212};// 把arr[5]初始化为212
int staff[] = {1, [6] = 4, 9, 10};
```

## 字符数组初始化
```c
char ch[10]={'\0'};//所有初始化为'\0'
char ch[100]={"hello"};//字符数组初始化
char ch[100]="hello";
char ch[]="hello";
```
# 多维数组
多维数组是一维数组的嵌套
# 变长数组(VLA)
VLA 是 C99 新增的特性
`int ar[n]`
- C90 不允许 n 为 const 类型
- C99/C11 允许 n 为 const 类型
- 变长数组不能初始化
- 变长数组必须为自动存储类别，离开所在块后即被释放；也就是说不能用 static 和 extern 关键字
- 变长数组创建完成后，长度不可改变；可变指的是创建时可以用变量指定数组的维度
# 数组与指针
1. 数组名是指向数组元素的指针，因为要用数组名遍历数组。
```c
int ar[10];
int num[10][10];
```
- ar 是 `int *`;
- `num[0]` 是 `int *`, `num` 是 `int (*)[10]`
2. 多维数组的低维可以看做高维的元素。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202308061945226.png)
