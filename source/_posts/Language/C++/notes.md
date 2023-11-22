---
title: C++
tags: []
categories:
  - Language
  - C++
---
标准的 C++ 由三个重要部分组成：
- 核心语言，提供了所有构件块，包括变量、数据类型和常量，等等。
- C++ 标准库，提供了大量的函数，用于操作文件、字符串等。
- 标准模板库（STL），提供了大量的方法，用于操作数据结构等。
deque:
- 初始化
```c++
deque<char> str{'A','B','#','D','#','#','C','#','#'};

char st[]="621##43###8##";
deque<char> str(st,st+strlen(st));
```
- 作为函数参数
```c++
void init(deque<char> *pstr, tree *pt);
init(&str, &t);
(*pstr).empty();
```
- 操作
```c++
str.empty()
str.front()
str.pop_front()
```