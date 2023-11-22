---
title: 数据结构和算法-线性表
tags:
  - algorithm
categories:
  - Data-Structure
mathjax: true
---

#  3.2 线性表的定义

线性表（list）：零个或多个数据元素的有限序列；
重点：数据元素不必是数字、有序、有限、唯一前驱唯一后继；
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307011942813.png)
线性表元素的个数 n ( n > 0 )定义为线性表的长度,当 n=0 时,称为空表。

# 3.3 线性表的抽象数据类型

创建和初始化、重置、根据位序得到数据元素、查找某个元素是否存在、获得线性表长度、插入数据和删除数据。

Page70/45
ADT 线性表 ( List )
Data
线性表的数据对象集合为 $\{a_1, a_2, ......, a_n\}$ 每个元素的类型均为 DataType。其中，除第一个元素 $a_1$ 外，每一个元素有且只有一个直接前驱元素，除了最后一个元素 $a_n$ 外，每一个元素有且只有一个直接后继元素。 数据元索之间的关系是一对一的关系。
```shell
Operation
InitList (*L):初始化操作 , 建立一个空的线性表
ListEmpty (L):若线性求为盒,返回 true ,否则返回 fal.se 。
ClearList (*L):
GetElem (L, i, *e*):
LocateElem (L, e):
ListInsert (*L, i, e):
ListDelete (*L, i, *e)
ListLength (L)
endADT
```

# 3.4 线性表的顺序存储结构

即数组；
线性表的顺序存储示意图如下:
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307012009441.png)

描述顺序存储结构的三个属性:
-  存储空间的起始位置：数组 data，它的存储位置就是存储空间的存储位置；
- 线性表的最大存储容量：数组长度 MaxSize 。
- 线性表的当前长度：length。

数据元素的序号和存放它的数组下标的对应关系
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307012016248.png)

假设每个数据元素占用的是 c 个存储单元,那么线性表中第 i+1 个数据元素的存储位置和第 i 个数据元素的存储位置满足下列关系( LOC 表示获得存储位置的函数)：
$$LOC(a_{i+1})=LOC(a_i)+c$$
所以对于第 i 个数据元素 $a_i$ 的存储位置可以由 $a_1$ 推算得出:
$$LOC(a_{i})=LOC(a_1)+(i-1)*c$$
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307012019963.png)

顺序存储结构的存取时间性能为O(1)

# 3.5 顺序存储结构的插入与删除

## 3.5.1 获得元素操作

sequence list

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307031016593.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307031017226.png)

## 3.5.2 插入操作
## 3.5.3 删除操作

# 3.6 线性表的链式存储结构

## 3.6.1 顺序存储结构不足的解决办法
## 3.6.2 线性表链式存储结构定义

link list

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307031035893.png)

因为此链表的每个结点中只包含一个指针域，所以叫做单链表

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307031040599.png)

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307031210832.png)

## 3.6.3 头指针与头结点的异同
## 3.6.4 线性表链式存储结构代码描述

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307031214667.png)

单链表中，我们在 C 语言中可用结构指针来描述。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307031215889.png)

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307031217757.png)

# 3.7 单链表的读取

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307031349122.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307031349647.png)

# 3.8 单链表的插入与删除

## 3.8.1 单链表的插入
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307031355551.png)

s->next=p->next ;p->next=s ;
解读这两句代码,也就是说让 p 的后继结点改成 s 的后继结点,再把结点 s 变成 p 的后继结点(如图 3-8-2 所示)。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307031356756.png)

## 3.8.2 单链表的删除

`p->next=p->next->next`
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307031402908.png)

# 3.9 单链表的整表创建

1. 头插法：始终让新结点在第一的位置。
2. 尾插法：把新结点都放到最后

# 3.10 单链表的整表删除
# 3.11 单链表结构与顺序存储结构优缺点
# 3.12 静态链表

定义：用数组来代替指针,来描述单链表。又名游标实现法。数组的元素都是由两个数据域组成, data 和 cur(即cursor).

另外我们对数组第一个和最后一个元素作为特殊元素处理, 不存数据。我们通常把未被使用的数组元素称为备用链表。而数组第一个元素,即下标为 0 的元素的 cur就存放备用链表的第一个结点的下标；而数组的最后一个元素的 cur 则存放第一个有数值的元素的下标,相当于单链表中的头结点作用,当整个链表为空时 , 则为 $0^2$ 。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307032108394.png)
假设我们已经将数据存入静态链表，比如分别存放着“甲” 、“乙”、“丁”，“戊”、“己”、“庚”等数据,则它将处于如图 3-12-2 所示这种状态。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307032113625.png)

## 3.12.1 静态链表的插入操作
## 3.12.2 静态链表的删除操作
## 3.12.3 静态链表优缺点

# 3.13 循环链表

将单链表中终端结点的指针端由空指针改为指向头结点，就使整个单链表形成一个环，这种头尾相接的单链表称为单循环链表，简称循环链表 ( circular linked list) 。

为了使空链表与非空链表处理一致，我们通常设一个头结点，当然，这并不是说，循环链表一定要头结点。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307042258735.png)

对于非空的循环链表就如图 3-13-4 所示 。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307042258432.png)

加快访问终端节点：用指向终端节点的尾指针rear表示链表。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307042302515.png)

合并循环列表：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307042310432.png)

# 3.14 双向链表

双向链表（double linked list）：是在单链表的每个结点中,再设置一个指向其前驱结点的指针域。所以在双向链表中的结点都有两个指针域, 一个指向直接后继 , 另一个指向直接前驱。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307042323663.png)

插入节点：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307042336516.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307042337937.png)

删除节点：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307042337087.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307042337310.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307042337763.png)
