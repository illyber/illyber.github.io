---
title: CSS-CSS盒子模型
categories:
  - Front-End
  - css
date: 2024-02-13 19:43:00
tags: 
updated:
---
# 学习目标
- 能够准确阐述盒子模型的4个组成部分
- 能够利用边框复合写法给元素添加边框
- 能够计算盒子的实际大小
- 能够利用盒子模型布局模块案例
- 能够给盒子设置圆角边框
- 能够给盒子添加阴影
- 能够给文字添加阴影
# 盒子模型
页面布局三大核心：盒子模型、浮动、定位
## 137-看透网页布局本质
网页布局过程:
1.先准备好相关的网页元素，网页元素基本都是盒子Box。
2.利用CSS设置好盒子样式，然后摆放到相应位置；
3.往盒子里面装内容.
## 138-盒子模型(box model)组成部分
CSS盒子模型本质上是一个盒子，封装周围的HTML元素，它包括：边框、外边距、内边距、和实际内容
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402132219431.png)

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402132219032.png)
## 边框 (border)
### 139-盒子模型边框border
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402140821227.png)

border可以设置元素的边框。边框有三部分组成:边框宽度(粗细)、边框样式、边框颜色
语法：
```html
border: border-width || border-style || border-color;
```

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402140825556.png)

边框样式：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402140830672.png)

```html
<html>
    <head>
        <title>盒子模型之边框</title>
        <style>
            div{
                width: 300px;
                height: 200px;
                /* 边框的粗细 */
                border-width: 5px;
                /* 边框的样式 solid实线、dashed虚线、dotted点线 */
                border-style: solid;
                /* 边框的颜色 */
                border-color: pink;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
</html>
```

### 140-边框的复合写法
语法：
```html
border: 1px solid red; 没有顺序
```

```html
<html>
    <head>
        <title>边框的复合写法</title>
        <style>
            div{
                width: 300px;
                height: 200px;
                border: 5px solid red;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
</html>
```

边框分段写法：
```html
border-top: 1px solid red; /*只设定上边框，其余同理*/
```

```html
<html>

<head>

<title>边框的复合写法</title>

<style>

div{

width: 300px;

height: 200px;

border: 5px solid red;

border-top: 10px dashed green;

}

</style>

</head>

<body>

<div></div>

</body>

</html>
```

### 141-表格细线边框
border-collapse 属性控制浏览器绘制表格边框的方式。它控制相邻单元格的边框。
语法：
```html
border-collapse: collapse;
```
- collapse 单词是合并的意思
- border-collapse: collapse; 表示相邻边框合并在一起而不是相加，变细
### 142-边框会影响盒子实际大小
设置盒子的宽和高不包括边框。
1. 测量盒子大小的时候，不量边框.
2. 如果测量的时候包含了边框，则需要width/height减去边框宽度

## 内边距 (padding)
### 143-盒子模型内边距padding
- padding 属性用于设置内边距，即边框与内容之间的距离.
- padding会撑大盒子
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402142309818.png)

### 144-padding复合属性
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402142331154.png)

### 145-padding会影响盒子实际大小
当我们给盒子指定padding值之后, 发生了2件事情:
1. 内容和边框有了距离，添加了内边距。
2. padding影响了盒子实际大小。
也就是说，如果盒子已经有了宽度和高度，此时再指定内边框，会撑大盒子.
解决方案：
如果保证盒子跟效果图大小保持一致，则让width/height减去多出来的内边距大小即可。

### 146-padding应用-新浪导航栏(上)
因为每个导航栏里面的字数不一样多,我们可以不用给每个盒子宽度了,直接给padding最合适.
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402151502217.png)

### 148-小米侧边栏修改
### 149-padding不会撑开盒子的情况
- 如果盒子本身没有指定width/height属性, 则此时padding不会撑开盒子大小.
- 只要有了width/height属性，到了极限还可以有滚动条

## 外边距 (margin)
### 150-盒子模型外边距margin
margin属性用于设置外边距，即控制盒子和盒子之间的距离。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402160015975.png)
margin简写方式代表的意义跟padding完全一致。
```html
margin: 30px 50px;
```
# PS基本操作
# 综合案例
# 圆角边框
# 盒子阴影
# 文字阴影