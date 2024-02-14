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
## 139-盒子模型边框border
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

## 140-边框的复合写法
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

边框分开写法：
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

## 141-表格细线边框
border-collapse 属性控制浏览器绘制表格边框的方式。它控制相邻单元格的边框。
语法：
```html
border-collapse: collapse;
```
- collapse 单词是合并的意思
- border-collapse: collapse; 表示相邻边框合并在一起而不是相加，变细
## 142-边框会影响盒子实际大小

# PS基本操作
# 综合案例
# 圆角边框
# 盒子阴影
# 文字阴影