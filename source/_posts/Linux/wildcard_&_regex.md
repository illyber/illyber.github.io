---
title: Shell-通配符和正则表达式
tags:
  - shell
  - wildcard
  - regex
categories:
  - Shell
---
[命令行通配符教程](https://www.ruanyifeng.com/blog/2018/09/bash-wildcards.html)

echo 没有找到对应文件名就按原样输出
# shell 开启通配符

- bash开启通配符
```shell
#开启通配符功能
shopt -s  extglob

#查看通配符功能是否开启，on表示已经开启
shopt -s
```

- zsh
```shell
# 开启*支持
setopt nonomatch
```

# 通配符字符

[命令行通配符教程 - 阮一峰](https://www.ruanyifeng.com/blog/2018/09/bash-wildcards.html)

通配符匹配文件名的时候不是用空格分开像字符串那样一起匹配，而是一个文件名一个文件名匹配。

除了 `{}` 以外，Bash 扩展通配符的时候，发现不存在匹配的文件，会将通配符原样输出。

```shell
*			    匹配任意多个字符，包括 0 个和 1 个。[0,∞)
？			    匹配任意 1 个字符一次，不包括空字符，不包括 0 个。[1,1]

[...]           匹配方括号之中的任意一个字符，比如[aeiou]可以匹配五个元音字母
[start-end]     表示一个连续的范围，匹配范围内的一个字符
[^...]和[!...]  匹配不在方括号里面的字符（不包括空字符）。这两种写法是等价的。
这种模式下也可以使用连续范围的写法[!start-end]

{...}与[...]有一个很重要的区别。如果匹配的文件不存在，[...]会失去模式的功能，变成一个单纯的字符串，而{...}依然可以展开。
{...} 			表示匹配大括号里面的所有模式，模式之间使用逗号分隔，模式可以是多字符的。
大括号可以嵌套。
大括号也可以与其他模式联用。
{start..end}会匹配连续范围的字符。
如果遇到无法解释的扩展，模式会原样输出。
```

```shell
$ echo {cat,d*}
cat dawg dg dig dog doug dug
```

posix 字符类

```shell
[:alnum:]	    匹配任意 1 个字母或数字
[:alpha:]		匹配任意 1 个字母
[:digit:]       匹配任意 1 个数字
[0-9]			匹配任意 1 个数字
[:lower:]		匹配任意 1 个小写字母
[:upper:]		匹配任意 1 个大写字母
```

# 正则表达式分类
1. 基本的正则表达式（Basic Regular Expression 又叫 Basic RegEx  简称 BREs）
2. 扩展的正则表达式（Extended Regular Expression 又叫 Extended RegEx 简称 EREs）
3. Perl 的正则表达式（Perl Regular Expression 又叫 Perl RegEx 简称 PREs）

# 元字符
![image-20220429223410456](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202306200026467.png)

# 修饰符
修饰符用在正则表达式结尾，例如：/dog/i，其中 “ i “ 就是修饰符，它代表的含义就是：匹配时不区分大小写，那么修饰符有哪些呢？常见的修饰符如下:

g   全局匹配（即：一行上的每个出现，而不只是一行上的第一个出现）  
s    把整个匹配串当作一行处理  
m    多行匹配  
i    忽略大小写  
x    允许注释和空格的出现  
U    非贪婪匹配
# linux正则表达式 (BREs,EREs,PREs) 差异比较
https://www.cnblogs.com/chengmo/archive/2010/10/10/1847287.html

# perl expression常用模式(pattern)
```shell
.    匹配除换行符（\n、\r）之外的任何单个字符，相等于 [^\n\r]。
x? 　 匹配 0 次或一次 x 字符串  
x* 　 匹配 0 次或多次 x 字符串，但匹配可能的最少次数  
x+ 　 匹配 1 次或多次 x 字符串，但匹配可能的最少次数  
.* 　 匹配 0 次或一次的任何字符  
.+ 　 匹配 1 次或多次的任何字符  

{m}　 匹配刚好是 m 个 的指定字符串  
{m,n} 匹配在 m个 以上 n个 以下 的指定字符串  
{m,}  匹配 m个 以上 的指定字符串  

[] 　 匹配符合 [] 内的字符  
[^]　 匹配不符合 [] 内的字符  
[0-9] 匹配所有数字字符  
[a-z] 匹配所有小写字母字符  
[^0-9]匹配所有非数字字符  
[^a-z]匹配所有非小写字母字符  

^ 　　 匹配字符开头的字符  
$ 　　 匹配字符结尾的字符  

\d　　 匹配一个数字的字符，和 [0-9] 语法一样  
\d+ 　匹配多个数字字符串，和 [0-9]+ 语法一样  
\D　　非数字，其他同 \d  
\D+　 非数字，其他同 \d+  

\w 　 英文字母或数字的字符串，和 [a-zA-Z0-9] 语法一样  
\w+ 　和 [a-zA-Z0-9]+ 语法一样  
\W 　 非英文字母或数字的字符串，和 [^a-zA-Z0-9] 语法一样  
\W+   和 [^a-zA-Z0-9]+ 语法一样  

\s    空格，和 [\n\t\r\f] 语法一样  
\s+   和 [\n\t\r\f]+ 一样  
\S    非空格，和 [^\n\t\r\f] 语法一样  
\S+   和 [^\n\t\r\f]+ 语法一样  

\b    匹配以英文字母,数字为边界的字符串  
\B    匹配不以英文字母,数值为边界的字符串

a|b|c 匹配符合a字符 或是b字符 或是c字符 的字符串  
abc   匹配含有 abc 的字符串
```
# 转义序列、posix字符类、中括号
参考：[regular tutorial - Posix Bracket Expressions]
```shell
\d
[:alpha:]
[a-z]
```

注意：`[` 和 `]` 是POSIX字符类本身的组成部分。
```posix
[[:digit:]]    任何数字
[:xdigit:]   任何十六进制数字

[:alpha:]    任何字母
[:lower:]    任何小写字母
[:upper:]    任何大写字母

[:alnum:]    任何字母或数字

[:cntrl:]    ASCII控制字符（ASCII 0~31 和 ASCII 127）

[:punct:]不属于[:alnum:]和[:cntrl:]的任何字符（标点符号）

[:blank:]空格或制表符（[\t ]）

[:space:]任何空白字符，包括空格（[\f\n\r\t\v ]）

[:print:]任何可打印字符

[:graph:]同[:print:],但不包括空格
```
