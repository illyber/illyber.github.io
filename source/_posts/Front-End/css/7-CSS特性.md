---
title: CSS-CSS特性
categories:
  - Front-End
  - css
date: 2023-11-17 00:00:00
tags:
updated:
---

<!-- toc -->

# 129-CSS特性-层叠性

2.1层叠性的介绍
特性:
1. 给同一个标签设置不同种类的样式->此时样式会层叠叠加->会共同作用在标签上
2. 给同一个标签设置相同种类的样式->此时样式会层叠覆盖->最终写在最后的样式会生效
注意点:
1. 当样式冲突时，只有当选择器优先级相同时，才能通过层叠性判断结果

# 18-CSS特性-继承性

1.1继承性的介绍
特性: 子元素有默认继承父元素样式的特点（子承父业）
可以继承的常见属性(文字控制属性都可以继承)
1. color
2. font-style、font-weight、font-size、font-family
3. text-indent、text-align
4. line-height
5. ...
注意点: 可以通过调试工具判断样式是否可以继承

1.2 继承失效：子元素自己有属性时


# 优先级
权重叠加：如果是复合选择器，则会有权重叠加，需要计算权重。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402110115570.png)
