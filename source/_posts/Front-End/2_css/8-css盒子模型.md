---
title: CSS-CSS盒子模型
categories:
  - Front-End
  - 2_css
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

### 151-外边距典型应用-块级盒子水平居中对齐
外边距可以让块级盒子水平居中，但是必须满足两个条件:
1. 盒子必须指定了宽度(width)
2. 盒子左右的外边距都设置为auto
常见的写法，以下三种都可以：
- `margin-left:auto; margin-right: auto;`
- `margin:auto;`
- `margin:0 auto;`

### 152-行内元素和行内块元素水平居中
注意: 以上方法是让块级元素水平居中，行内元素或者行内块元素水平居中给其父元素添加text-align:center即可。看作文字
```html
<html>
    <head>
        <title>行内元素和行内块元素水平居中</title>
        <style>
            .header{
                width: 900px;
                height: 200px;
                background-color: pink;
                margin: 0 auto;
                text-align: center;
            }
        </style>
    </head>
    <body>
        <div class="header">
            <span>里面的文字</span>
        </div>
    </body>
</html>
```

### 153-外边距合并-嵌套块元素塌陷
使用margin定义块元素的垂直外边距时，可能会出现外边距的合并。
对于两个嵌套关系(父子关系)的块元素，父元素有上外边距同时子元素也有上外边距，此时父元素会塌陷较大的外边距值.
```html
<html>
    <head>
        <title></title>
        <style>
            .father{
                width: 400px;
                height: 400px;
                background-color: purple;
                margin-top: 50px;
            }
            .son{
                width: 200px;
                height: 200px;
                background-color: pink;
                margin-top: 100px;
            }
        </style>
    </head>
    <body>
       <div class="father">
            <div class="son"></div>
       </div> 
    </body>
</html>
```

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402191940495.png)
解决方案：
- 可以为父元素定义上边框。`border: 1px solid transparent; /*transparent 透明的*/`
- 可以为父元素定义上内边距。`padding: 1px;`
- 可以为父元素添加 overflow:hidden;优点：不会改变盒子大小。
### 154-清除内外边距
网页元素很多都带有默认的内外边距。而且不同浏览器默认的也不一致。因此我们在布局前，首先要清除下网页元素的内外边距。
```html
*{
	padding:0; /*清除内边距*/
	margin:0;  /*清除外边距*/
}
```
注意：行内元素为了照顾兼容性，尽量只设置左右内外边距，不要设置上下内外边距。但是转换为块级和行内块元素就可以了。
# PS基本操作
字节用的figma吗？
测量元素长度：
- 文件→打开：可以打开我们要测量图片
- Ctrl+R：可以打开标尺，或者视图→标尺
- 右击标尺，把里面的单位改为像素
- Ctrl+加号(+)可以放大视图，Ctrl+减号(-)可以缩小视图
- 按空格，鼠标变成小抓手，可以移动图片
- 用选区拖动可以测量大小
- Ctrl+D可以取消选区，或者在旁边空白处点击一下也可以取消选区
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402271738388.png)

# 综合案例
## 156-综合案例-产品模块布局分析
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402271800899.png)

## 157-综合案例-box布局


# 圆角边框
# 盒子阴影
# 文字阴影