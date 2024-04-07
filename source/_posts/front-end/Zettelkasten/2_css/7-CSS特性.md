---
title: CSS-CSS特性
categories:
  - Front-End
date: 2023-11-17 00:00:00
tags:
updated:
---

<!-- toc -->

# 129-CSS特性-层叠性

2.1层叠性的介绍
特性:
1. 给同一个标签设置不同种类的样式->此时样式会层叠叠加->会共同作用在标签上
2. 给同一个标签设置相同种类的样式->此时样式会层叠覆盖->最终写在最后的样式会生效（就近原则）
注意点:
1. 当样式冲突时，只有当选择器优先级相同时，才能通过层叠性判断结果
```html
<html>
<head>
    <title>Document</title>
    <style>
        div{
            color: red;
            color: green;
        }
        .box{
            font-size: 30px;
        }
    </style>
</head>
<body>
    <div class="box">
        文字
    </div>
</body>
</html>
```

# 130-CSS特性-继承性

1.1继承性的介绍
特性: 子元素有默认继承父元素样式的特点（子承父业）
可以继承的常见属性(文字控制属性都可以继承)
1. color
2. font-style、font-weight、font-size、font-family
3. text-indent、text-align
4. line-height
5. ...
注意点: 可以通过调试工具判断样式是否可以继承
高度，内外边距等不能继承。高度可以继承？宽度可以继承，但只有块元素可以继承
```html
<html lang="en">
<head>
    <title>Document</title>
    <style>
        div{
            color: red;
        }
    </style>
</head>
<body>
    <div>
        div里的文字
        <span>div里的span</span>
    </div>
</body>
</html>
```

1.2 继承失效：子元素自己有属性时
1.3 行高的继承性
```html
body{
    font: 12px/1.5 'Microsoft YaHei';
    /* 1.5倍行高 */       
            }
```
1.4 如果元素没有指定宽度，则继承父亲的宽度

# 132-css特性-优先级
```html
<html>
    <head>
        <title>css优先级</title>
        <style>
            div{
                color: pink;
            }
            .test{
                color: red;
            }
        </style>
    </head>
    <body>
        <div class="test">你笑起来真好看</div>
    </body>
</html>
```
当同一个元素指定多个选择器，就会有优先级的产生。
- 优先级高的选择器不会覆盖所有低优先级选择器的内容，只会覆盖相同类型的属性
- 选择器相同，则执行层叠性
- 选择器不同，则根据选择器权重执行。选择器权重如下所示：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402131737932.png)
- !important的使用方法
```html
div{
    color: pink!important;
    }
```

```html
<html>
    <head>
        <style>
            #father {
                color: red;
            }
            p{
                color: pink;
            }
        </style>
    </head>
    <body>
        <div id="father">
            <p>你真漂亮</p>
        </div>
    </body>
</html>
```

- 继承的权重最低，加!important也不起作用
- a链接浏览器默认指定了一个样式，继承父元素的不管用。
```html
<html>
    <head>
        <style>
            body{
                color: red;
            }
        </style>
    </head>
    <body>
        <a href="#">我是单独的样式</a>
        <!-- 仍为蓝色，因为a自己有默认属性（蓝色+下划线），比继承权重高 -->
    </body>
</html>
```
- 如果是复合选择器，则会有权重叠加，需要计算权重。
- 权重是有4组数字组成，但是不会有进位。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202402110115570.png)
```html
<html>
    <head>
        <title>权重练习</title>
        <style>
            .nav li{
                color: red;
            }
            .pink{
                color: pink;
                font-size: 20px;
            }
        </style>
    </head>
    <body>
        <ul class="nav">
            <li class="pink">第一行</li>
            <li>第二行</li>
        </ul>
    </body>
</html>
```