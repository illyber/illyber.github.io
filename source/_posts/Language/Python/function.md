---
title: Python 函数
tags:
  - python
categories:
  - Language
  - Python
---
# def 语句和参数
```python
def hello(name):
    print('Hello ' + name)
hello('Alice')
hello('Bob')
```
# 返回值和 return 语句
用 def 语句创建函数时，可以用 return 语句指定应该返回什么值。return 语句包含以下部分：
- return 关键字;
- 函数应该返回的值或表达式。
return 可以返回字符串
# None 值
None 表示没有值。None 是 NoneType 数据类型的唯一值(其他编程语言可能称这个值为 null、nil 或 undefined)。

在幕后,对于所有没有 return 语句的函数定义,Python 都会在末尾加上 return None；如果使用不
带值的 return 语句(也就是只有 return 关键字本身)，那么就返回 None。
# 关键字参数和 print()
大多数参数是由它们在函数调用中的位置来识别的；“关键字参数”是由函数调用时加在它们前面的关键字来识别的。

print()函数有可选的变元 end 和 sep.
print()函数自动在传入的字符串末尾添加了换行符。可以设置 end 关键字参数,将它变成另一个字符串。

如果向 print()传入多个字符串值,该函数就会自动用一个空格分隔它们。
```python
>>> print('cats', 'dogs', 'mice')
cats dogs mice
```
可以传入 sep 关键字参数,替换掉默认的分隔字符串。
```python
>>> print('cats', 'dogs', 'mice', sep=',')
cats,dogs,mice
```
# 局部和全局作用域
如果在不同的作用域中，你可以用相同的名字命名不同的变量。
# global 语句
如果需要在一个函数内修改全局变量，就使用 global 语句。如果在函数的顶部有 global eggs 这样的代码，它就告诉 Python,“在这个函数中，eggs 指的是全局变量，所以不要用这个名字创建一个局部变量。”
```python
def spam():
    global eggs
    eggs = 'spam'
eggs = 'global'
spam()
print(eggs)
```
# 异常处理
错误可以由 try 和 except 语句来处理。那些可能出错的语句被放在 try 子句中。如果错误发生,程序执行就转到接下来的 except 子句开始处。
如果在 try 子句中的代码导致一个错误,程序执行就立即转到 except 子句的代码。在运行那些代码之后,执行照常继续。
```python
def spam(divideBy):
    try:
        return 42 / divideBy
    except ZeroDivisionError:
        print('Error: Invalid argument.')
print(spam(2))
print(spam(12))
print(spam(0))
print(spam(1))
```