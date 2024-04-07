---
title: lua-B站网课笔记
date: 2024-04-04 21:15
tags:
  - lua
categories:
---
---
# 环境、注释
[【无废话30分钟】Lua快速入门教程 - 4K超清](https://www.bilibili.com/video/BV1vf4y1L7Rb/?spm_id_from=333.337.search-card.all.click&vd_source=4f8ddad44fd904574089cafb91e9e009)
编程环境：
- luatos->在线体验luatos
- 安装lua解释器：`sudo apt install lua`
```lua
--交互式编程
lua or lua -i
--脚本编程
lua script.lua
--在脚本内指定解释器
#!/usr/local/bin/lua
./script.lua
```
末尾不用加分号
资料：lua参考手册
单行注释
```lua
--这是单行注释
```
多行注释
```lua
--[[
 多行注释
 多行注释
 --]]
```
# print
- 打印字符串
```lua
print("hello world!")
```
- 分别打印两个变量
```lua
print(a,b)
```
- 打印两变量之和
```lua
print(a+b)
```

# 变量
## 变量声明
赋值一个变量就相当于新建了一个变量。和shell一样
```lua
a=1
```

lua声明的变量默认是全局变量，可以跨文件引用。

local关键字声明局部变量。只能在当前的函数、代码块、文件里引用。
```lua
local a = 1
```
## 多重赋值
下式给a赋1，给b赋2
```lua
a,b = 1,2
```

右边的数不够，左边未被赋值的仍是nil
下面的c仍是nil
```lua
a,b,c = 1,2
```
## 变量类型
### nil类型
没有被声明过的变量都是nil。nil变量的值只有nil

```lua
print(c)
c是一个没有被声明过的变量

输出
nil
```
### 数值型
没有int float之分，所有数值都是数值型
声明方式：
- 普通：
```lua
a = 1
```
- 十六进制表示法：
```lua
a = 0x11
```
- 科学记数法，下面表示 $2\times 10^{10}$：
```lua
a = 2e10
```

![[#算术运算符]]
### 字符串
单引号或者双引号括住字母
```lua
str = "hello world"
--or--
str = 'hello world'
```

支持转义字符。`\n`会被打印成换行
```lua
str = 'hello\nworld'
```

多行文本和原样文本。
两对中括号里可以表示任意原样文本，甚至换行也可以，里面的转义字符不会被转义。
```lua
c = [[hello
\n

world
dddd]]
```

连接字符串
```lua
c = a..b
```

数字转字符串：tostring
a里面是字符串"10"
```lua
a = tostring(10)
```

字符串转数字：tonumber
tonumber转换失败的结果是nil
```lua
n = tonumber("100")
```
下面的结果就是nil
```lua
tonumber("abc")
```

字符串长度：前面加井号
转义字符转义后算一个字符
```lua
str = "hello "
print(#str)
```

ASCII码值转字符串：string.char()
```lua
s = string.char(0x30, 0x31, 0x32, 0x33)
print(s)
```

返回字符串指定位的ASCII码值：string.byte()
```lua
s = string.char(0x30, 0x31, 0x32, 0x33)
c = string.byte(s,2)
print(c)
```

可以在字符串中存放`\0`，不代表字符串的结束
### 布尔型
值只有true和false两种情况。
只有false和nil表示假，其他都是真，0也表示真。
```lua
a,b = true,false
print(a,b)

输出：
true	false
```

# 运算符
## 算术运算符
加减乘除
乘方(^)
左移(<<)右移(>>)
```lua
print(1<<3)

结果是8
```
## 字符串连接符号
两个点
```lua
c = a..b
```
## 关系运算符

| 含义   | 运算符           |
| ---- | ------------- |
| 大于   | `>`           |
| 小于   | `<`           |
| 大于等于 | `>=`          |
| 小于等于 | `<=`          |
| 等于   | <kbd>==</kbd> |
| 不等于  | <kbd>~=</kbd> |
关系表达式的值是true或false
## 逻辑运算符
返回值：读取到哪个值能判断整个表达式的真假就返回那个值

| 含义  | 运算符 | 返回值类型        | 返回值                             |
| --- | --- | ------------ | ------------------------------- |
| 与   | and | 不是true false | 第一个是假返回第一个，第一个是真返回第二个           |
| 或   | or  | 不是true false | 两个都是真返回第一个值，有一个真就返回真的值，全假返回第二个值 |
| 非   | not | 是true false  | true或false                      |
- 只有false和nil表示假，其他都是真，0也表示真。
- 逻辑表达式的值不只是true false
```lua
a,b = nil,0
--nil 假
--0   真
print( a and b )
print( a or b )
print( not a )

输出：
nil
0
true
```
短路求值（or的优先级更高？）
```lua
b=11
print(b>10 and "yes" or "no")
```
# 函数
## 声明
```lua
function 函数名(函数参数	)
	函数体
end
```
也可以把函数名放在function前面，后加等号
```lua
函数名=function(函数参数)
	函数体
end
```

函数的返回值默认是nil
可以用return主动返回值。return可以返回多个值。
多个返回值搭配多重赋值语句。
```lua
function f( a,b,c )
    return a,b
end
print(f(1,2,3))
```

# table
## 数字下标 table
### 声明
可以存数字、字符串、另一个table、函数。用逗号分隔。
```lua
t = {1,"fox",{},function() end}
```

### 引用
下标从1开始。
方括号里放下标引用
```lua
t = {1,"fox",{},function() end}
print(t[1])
```

越界，引用nil

### 赋值
可以越界赋值
```lua
t = {1,"fox",{},function() end}
t[5]=66
```

### table长度
前加井号
```lua
t = {1,"fox",{},function() end}
print(#t)
```
下标不连续，后面元素不计入数组元素总个数。

### 插入 table.insert()
在table末尾插入
```lua
t = {1,"fox",{},function() end}
table.insert(t,"d")
```

在第二位插入。
"fox"等元素后移一位。
```lua
t = {1,"fox",{},function() end}
table.insert(t,2,"d")
```

### 移除table.remove()
移除第二个。
后面的元素前进一位。
table.remove()返回移除的元素。
```lua
t = {1,"fox",{},function() end}
table.remove(t,2)
```

## 字符串下标
### 定义
逗号分隔
```lua
a = {
    a = 1,
    b = "1234",
    c = function()
	end,
	d = 123123
}
```
### 引用
没有声明过的下标，值一定是nil
- 双引号
```lua
a = {
    a = 1,
    b = "1234",
    c = function()
	end,
	d = 123123
}
print(a["a"])
```
- 点
```lua
a = {
    a = 1,
    b = "1234",
    c = function()
	end,
	d = 123123
}
print(a.a)
print(a.b)
```
- 不符合变量命名规范（这里不太懂）
```lua
a = {
    a = 1,
    b = "1234",
    c = function()
	end,
	[",;"] = 123123
}
print(a[",;"])
```
## 赋值
同样可以越界赋值
```lua
a = {
    a = 1
}
a["abc"] = "nicefox"
print(a["abc"])
print(a.abc)
```

## 全局表 `_G`
### 特殊性
所有的全局变量都在_G这个table里
```lua
print(_G)

输出：
table: 0x3
```

table.insert()。table是一个表，insert可以看作它的下标，它的值就是insert函数。table这个表含有insert, remove等一共十个下标/元素。
```lua
print(_G["table"])
print(_G["table"]["insert"])

输出：
table: 0x10
function: 0x155
```
### 引用
用字符串下标引用
```lua
a=1
b=2
print(_G["a"])
```

# 控制流
## 分支判断
```lua
if 1>10 then
	print("1>10")
else
	print("no")
end
```
- 不能缺then和end。end表示结束，就和函数里一样。
- 支持if, if else, if elseif, if elseif else.
- if 和 elseif 条件后要加then
```lua
if 1>10 then
	print("1>10")
elseif 1<10 then
    print("1<10")
else
	print("no")
end
```

## 循环
### for
基本形式
```lua
for i=1,10 do
	print(i)
end
```
可以设置步长（可以是负数），默认步长是 1。下面不会打印 10.
```lua
for i=1,10,2 do
	print(i)
end
```
break
```lua
for i=1,10 do
	print(i)
	if i==5 then break end
end
--then...end和do...end 相当于花括号
```
关于 i
- i 是循环这一部分的局部变量。
- i 在运行过程中无法手动更改。
- 在循环体里对 i 赋值，不会更改计数。对 i 的引用赋值与计数器是隔开的，相当于 local i
```lua
for i=1,10 do
	print(i)
	i=1
	print(i)
end
```

### while
基本形式
```lua
local n=10
while n>1 do
    print(n)
    n=n-1
end
```
break
```lua
local n=10
while n>1 do
    print(n)
    n=n-1
    if n==5 then break end
end
```
### repeat




---