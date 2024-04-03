---
title: 数据结构和算法-复杂度
tags:
  - algorithm
categories:
  - Data-Structure
mathjax: true
---
# 二分查找binary search

- n 次查找能处理的数据：
$$
2^n-1
$$

# 等比数列
- 定义：

$$
a_1,\ a_1q,\ a_1q^2,\ ...\ ,a_1q^{n-1}\\
$$

- 通项公式：

$$
a_n=a_1q^{n-1}
$$

- 前n项和：

$$
S_n=\frac{a_nq-a_1}{q-1}=a_1\times\frac{q^n-1}{q-1}
$$

计算前n项和就是在计算 $a_1\times(111···111)_q$
# 级数
- 几何级数
$$\sum_{i=0}^N A^i=\frac{A^{N+1}-1}{A-1}$$
若 $0<A<1,$
$$\sum_{i=0}^N A^i \leq \frac{1}{1-A}$$
$$\lim_{N\rightarrow\infty} \sum_{i=0}^N A^i = \frac{1}{1-A}$$
- 几何级数扩展
$$\sum_{i=0}^n iA^i=[nA^{n+1}-(n+1)A^n+1]\cdot\frac{A}{(A-1)^2}$$
- 算术级数
$$\sum_{i=1}^N i = \frac{N(N+1)}{2} \approx \frac{N^2}{2}$$
$$\sum_{i=1}^N i^2 = \frac{N(N+1)(2N+1)}{6} \approx \frac{N^3}{3}$$
$$\sum_{i=1}^N i^k \approx \frac{N^{k+1}}{|k+1|};\ k \neq -1$$
- 调和级数
$$H_N = \sum_{i=1}^N \frac{1}{i} \approx \log_eN$$
# 进制
## 结构图
- Positional notation/positional numeral system
- base/radix: In a positional numeral system, the radix or base is the number of unique digits.

假设当前数字是 N 进制，那么：
- 对于整数部分，从右往左看，第 i 位的位权(palce weight)等于 $N^{i-1}$
- 对于小数部分，恰好相反，要从左往右看，第 j 位的**位权**为 $N^{-j}$

更加通俗的理解是，假设一个多位数（由多个数字组成的数）某位上的数字是 1，那么它所表示的数值大小就是该位的位权。

![img](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202302140128346.png)

## [进制转换](http://c.biancheng.net/view/1725.html)

# [整数、分数及小数的英文读法](https://zhuanlan.zhihu.com/p/136783132)

## 整数的读法

和中文四位一节不同，英文是三位一节(period)，加逗号隔开：
- 4,321 四千三百二十一 four thousand, three hundred twenty-one

This is a four-digit number (四位数), where the digit 1 is in the ones place (个位), standing for 1 one (1个一) the digit 2 is in the tens place (十位), standing for 2 tens (2个十), the digit 3 is in the hundreds place (百位), standing for 3 hundreds (3个百), and the digit 4 is in the thousands place (千位), standing for 4 thousands (4个千).

# 对数(Logarithm)
The logarithm is denoted "$\log_b x$" (pronounced as "the logarithm of *x* to base *b*", "the base-*b* logarithm of *x*", or most commonly "the log, base b, of x").
# 排列组合
- 分类原理/加法原理
- 分步原理/乘法原理

- 排列：
$$A_n^m=n(n-1)\cdots [n-(m-1)]=\frac{n!}{(n-m)!}$$
已经占用了 m-1 个位置。

- 组合：
$$C_n^m=\frac{A_n^m}{A_m^m}=\frac{n(n-1)\cdots [n-(m-1)]}{m!}=\frac{n!}{(n-m)!\cdot m!}$$
