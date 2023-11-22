---
title: 数据结构和算法-栈与队列
tags:
  - algorithm
categories:
  - Data-Structure
mathjax: true
---

# 4.2 栈的定义

## 4 .2 . 1 栈的定义
栈( stack )是限定仅在表尾进行插入和删除操作的线性表。
我们把允许插入和删除的一端称为枝顶（top） ,另一端称为栈底（bottom），不含任何数据元素的栈称为空栈。栈又称为后进先出( Last In First Out)的线性表,简称 LIFO 结构 。

例子：
- 浏览器后退
- 软件的撤销操作

栈的插入操作,叫作进栈（push）,也称压栈、入栈。 
栈的删除操作,叫作出栈（pop） , 也有的叫作弹栈。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050003145.png)

## 4 .2.2 进拔出校变化形式

# 4.3 栈的抽象数据类型

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050009144.png)

# 4.4 栈的顺序存储结构及实现

## 4.4.1 栈的顺序存储结构
顺序栈

栈的结构定义：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050016010.png)

栈普通情况、空栈和栈满的情况示意图如图4-4-2 所示 。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050017076.png)

## 4.4.2 栈的顺序存储结构一一进栈操作
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050023019.png)

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050024255.png)

## 4 .4. 3 栈的顺序存储结构一一出栈操作
出栈操作pop代码
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050025551.png)

# 4.5 两栈共享空间

我们的做法如图 4-5-1，数组有两个端点，两个栈有两个栈底，让一个栈的栈底为数组的始端，即下标为 0 处，另一个栈底为数组的末端，即下标为数组长度 n - 1 处。这样，两个栈如果增加元素，就是从两端点向中间延伸。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050037253.png)

两栈共享空间的结构的代码如下：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050040962.png)

两栈共享空间的 push 方法：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050041179.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050041039.png)

两栈共享空间 的 pop 方法：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050042036.png)

# 4.6 栈的链式存储结构及实现

## 4 . 6 . 1 栈的链式存储结构
链栈
把栈顶放在单链表的头部(如图 4-6-1 所示) ，通常对于链栈来说,是不需要头结点的。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050057404.png)

链栈的结构代码如下 :
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050103395.png)

## 4.6.2 栈的链式存储结构一一进栈操作
对于链栈的进栈 push 操作,假设元素值为 e 的新结点是 s, top 为栈顶指针, 示意图如图 4-6-2 所示代码如下 。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050115260.png)

# 4.8 栈的应用一一递归

## 4 .8.1 斐波那契数列实现
数组or函数递归
常规的迭代办法
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050139705.png)

斐波那契的递归函数:
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050140197.png)
i=5 时的计算过程：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050141394.png)

## 4.8.2 递归定义
选代和递归的区别是:迭代使用的是循环结构,递归使用的是选择结构。递归更消耗资源。

# 4.9 栈的应用一一四则运算表达式求值

## 4.9.1 后缀(逆波兰)表示法定义
不需要括号的后缀表达法,我们也把它称为逆波兰( Reverse Polish Notation , RPN) 表示，所有的符号都是在要运算数字的后面出现
```c
9 + (3-1)×3 + 10÷2
9 3 1-3 * + 10 2 / +
```

## 4.9 .2 后缀表达式计算结果
规则:从左到右遍历表达式的每个数字和符号,遇到是数字就进栈,遇到是符号,就将处于栈顶两个数字出栈,进行运算,运算结果进栈, 一直到最终获得结果。

## 4.9.3 中缀表达式转后缀表达式
我们把平时所用的标准四则运算表达式 ,即“9+ ( 3-1 )× 3+10÷2 " 叫做中缀表达式。因为所有的运算符号都在两数字的中间。
规则 : 从左到右遍历中缀表达式的每个数字和符号,若是数字就输出,即成为后缀表达式的一部分 ; 若是符号,则判断其与栈顶符号的优先级 , 是右括号或优先级低于栈顶符号(乘除优先加减)则栈顶元素依次出栈并输出,并将当前符号进栈,一直到最终输出后缀表达式为止。

要想让计算机具有处理我们通常的标准(中缀)表达式的能力,最重要的就是两步:
1. 将中缀表达式转化为后缀表达式 (栈用来进出运算的符号) 。
2. 将后缀表达式进行运算得出结果 (栈用来进出运算的数字)。

# 4.10 队列的定义

队列 ( queue ) 是只允许在一端进行插入操作,而在另一端进行删除操作的线性表。
队列是一种先进先出( First In First Out)的线性表,简称 FIFO 。允许插入的一端称为队尾,允许删除的一端称为队头。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050208657.png)

# 4.11 队列的抽象数据类型

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307050210927.png)

# 4.12 循环队列

## 4.12.1 队列顺序存储的不足
不足：出队时间复杂度为O(n)
解决办法：队头不一定在下标为0的位置
front 指针指向队头元素 , rear 指针指向队尾元素的下一个位置,这样当 front 等于 rear 时,此队列不是还剩一个元素,而是空队列。

## 4.12 .2 循环队列定义
我们把队列的这种头尾相接的顺序存储结构称为循环队列。

如何判断循环队列究竟是空还是满：
- 办法一是设置一个标志变量 flag , 当 front == rear ,且 flag= 0 时为队列空,当 front = = rear,且 flag= 1 时为队列满；
- 办法二是当队列空时,条件就是 front == rear ,当队列满时,我们修改其条件,保留一个元素空间。也就是说,队列满时,数组中还有一个空闲单元 。例如图 4- 12-8 所示,我们就认为此队列已经满了,也就是说,我们不允许图4-12-7 的右图情况出现。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307051250666.png)

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307051250670.png)

队列满的条件是：$$(rear+1) \% QueueSize == front$$
通用的计算队列长度公式为：$$( rear- front+ QueueSize) \%QueueSize $$

# 4.13 队列的链式存储结构及实现

为了操作上的方便,我们将队头指针指向链队列的头结点，而队尾指针指向终端节点,如图 4-13 -1 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307051309500.png)

空队列时，front 和 rear 都指向头结点,如图 4- 1 3-2 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307051309148.png)

## 4.13.1 队列的链式存储结构一一入队操作
入队操作时,其实就是在链表尾部插入结点 ,如图 4-13-3 所示。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307051311880.png)

## 4.13.2 队列的链式存储结构一一出队操作
若链表除头结点外只剩一个元素时, 则需将 rear 指向头结点
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307051315296.png)

代码如下：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307051316291.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307051316671.png)
