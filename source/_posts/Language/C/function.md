---
title: 函数
tags:
  - C
categories:
  - Language
---
# parameter与argument辨析

虽然常常混用，但C99规定，parameter是形式参数；argument是实际参数，也就是函数调用传递的值。

# 命令行参数 P311

- main() 接收命令行参数：`int main( int argc, char *argv[])`

- 名为 repeat 的 C 可执行程序在命令行这样接受参数：$ ./repeat Resistance
- argc（即 argument count）表示命令行中的字符串数量（包括命令名），以空格分割字符串；上面命令的参数数量为 2；
- argv（即 argument value）存放每个字符串的地址，argv[0] 存放命令名（即 "repeat"）的地址。