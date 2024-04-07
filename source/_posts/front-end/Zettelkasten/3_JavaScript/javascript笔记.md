---
title: javascript笔记
date: 2024-04-06 06:43
tags:
  - javascript
categories:
---
---
javascript 是网景开发的语言，之所以取名为javascript不是因为和java有什么关系，而是因为方便传播和项目有 SUN 公司参与。

# js的导入方式
1. 内联式：直接写在 html 文件里，`<script></script>`标签内。script 标签既可以在 head 标签里，也可以在 body 标签里。
```js
<script>console.log("hello world!")</script>
```
 2. 外部导入：用 script 标签的 src 属性引入。文件后缀一般为 js
```js
<script src=""></script>
```

# hello world
运行环境：浏览器
输出的位置：`F12`->console

- console.log
```js
console.log("hello world!")

//打印多个变量
var x=1;let y=2;const Pi=3.14;
console.log(x, y, Pi)
```


console.log 在控制台打印日志内容。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/20240406220032.png)

弹窗打印：
```js
alert("alert function")
```
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/20240406222505.png)

# 变量
## 声明变量

|       | 说明                   | 例子               |
| ----- | -------------------- | ---------------- |
| var   | 变量具有函数作用域。避免使用 var   | `var x=1;`       |
| let   | 变量具有块级作用域。let 更安全灵活。 | `let y=5;`       |
| const | 声明常量                 | `const Pi=3.14;` |

变量未初始化，值是 undefined。函数没有返回值的时候，返回的也是 undefined

声明字符串
```js
let name="myname";
```

声明空值
```js
let empty_value=null;
```

## 作用域

函数作用域：在函数结构体内定义的变量。这与 C 语言不同，C 语言的函数作用域是在函数头。
全局作用域：在函数外定义的变量。

# 控制流
## 条件语句

if 语句
```js
if (condition){
	//...
}
```

else 语句
```js
if (condition){
	//...
} else{
	//...
}
```

else if 语句
```js
if (condition1){
	//...
} else if (condition1){
	//...
}
...
else{
	//...
}
```

## 循环语句

for 语句
```js
for (初始化表达式; 循环条件; 迭代器){
	//...
}
```

while 语句
```js
while (循环条件){
	//...
}
```

break 和 continue 关键字
break: 跳出整个循环
continue: 跳过剩余代码，进行下一次循环。
```js
for (let i = 0; i < 7; i++) {
    if(i==2) continue;
    if(i==5) break;
    console.log(i);
}
```

# 函数
```js
function function_name(arg1, arg2, arg3, ...){
	//函数体
	return 返回值;
}
```

打印hello world
```js
function print_hello() {
    console.log("hello world!");
}
print_hello();
```

可以返回字符串
```js
function print_hello() {
    return "返回 hello world!";
}
let str=print_hello();
console.log(str);
console.log(print_hello());
```

带形参，拼接字符串。
```js
function hello_with_params(name){
    console.log("hello, "+name);
}
hello_with_params("Tom");
```

# 事件
## 定义和种类
事件就是文档或者浏览器窗口中发生的特定瞬间。是函数触发的条件。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/20240407145625.png)
绑定事件的三种方法：
1. `HTML`属性
2. `DOM`属性
3. `addEventListener`方法
## html 属性添加
- 点击事件
```js
<button onclick="click_event()">点击事件按钮</button>
<script>
    function click_event() {
        alert('点击事件触发了');
    }
</script>
```

- 聚焦/失焦
```js
<input type="text" onfocus="focus_event()" onblur="blur_event()">
<script>
    function focus_event() {
        console.log('获取焦点');
    }
    function blur_event() {
        console.log('失去焦点');
    }
</script>
```

## DOM 添加
当网页被加载时，浏览器会创建页面的文档对象模型，也就是DOM(Document Object Model)。
每个HIML或XML文档都可以被视为一个文档树，文档树是整个文档的层次结构表示。
文档节点是整个文档树的根节点。
DOM为这个文档树提供了一个编程接口，开发者可以使用JavaScript来操作这个树状结构。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/20240407160118.png)

通过DOM引用节点
id 是唯一的，class 和 tag 不是唯一的所以返回数组。
```js
<div id="box1">这是一个id选择器标签</div>
<div class="box2">这是一个类选择器标签</div>
<div>普通的div标签</div>
<script>
    // 通过id获得元素
    let element_id = document.getElementById('box1');
    console.log(element_id);

    // 通过类名获得元素
    // 返回值是一个数组，要用下标引用
    let element_class = document.getElementsByClassName('box2')[0];
    console.log(element_class);

    // 返回值是一个数组，要用下标引用
    let element_tag = document.getElementsByTagName('div');
    console.log(element_tag);
</script>
```
结果：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/20240407162034.png)

通过DOM修改节点
```js
<div id="box1">这是一个id选择器标签</div>
<div class="box2">这是一个类选择器标签</div>
<div>普通的div标签</div>
<script>
    let element_id = document.getElementById('box1');
    console.log(element_id);

    let element_class = document.getElementsByClassName('box2')[0];
    console.log(element_class);

    let element_tag = document.getElementsByTagName('div')[2];
    console.log(element_tag);

    // 修改节点
    element_id.innerHTML = '<a href="#">跳转链接</a>';
    //innerText会忽略html标记，不会解析
    element_class.innerText = '<a href="#">跳转链接</a>';
    // 添加属性
    element_tag.style.color = 'red';
</script>
```
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/20240407163036.png)

通过DOM绑定事件
```js
<button>点击按钮</button>
<script>
    let button_element = document.getElementsByTagName('button')[0];
    // 赋的是匿名函数，没有函数名
    button_element.onclick = function(){
        alert('DOM属性 按键触发');
    }
</script>
```

## addEventListener 添加
```js
<button>点击按钮</button>
<script>
    let button_element = document.getElementsByTagName('button')[0];

    button_element.addEventListener('click', function(){alert('addEventListener 添加点击事件')});
</script>
```















---