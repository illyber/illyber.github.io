---
title: sed
date: 2024-04-02 05:20
tags:
  - 文本处理
categories:
  - Linux
---

---
# 命令结构

sed默认不修改原文件，而是把修改后的文件打印到标准输出。
命令行里，地址命令要用单引号引起来；脚本里不用引起来。和 awk 类似。
可以有多组地址命令，在命令行里时要用分号隔开；在脚本里要换行.
```shell
sed [option] '/[regexp]/[cmd][action]' filename
sed 选项 '地址 命令'	文件名
sed 选项 '地址 命令;地址 命令;地址 命令;...'	文件名
sed -f 脚本 文件名
```
下面是一个脚本例子
```bash
1i2024 0331 20:43\nTags: #脚本/\n\n---\n                               
$G
$a --- 
```

命令行里使用时要在地址和命令外加单引号，脚本里不能加单引号。
# 修改原文件 -i
-i 选项
# 使用脚本 -f
-f 选项
脚本里的操作不能加单引号。
```bash
1i2024 0331 20:43\nTags: #脚本/\n\n---\n                               
$G
$a --- 
```
# 不输出原文件内容 -n
sed -n '/hello/p'
# 单引号
单引号里的 `\n` 会被
# 地址

| 位置      | 表示                          |
| ------- | --------------------------- |
| 最后一行    | $                           |
| 第一行     | 1                           |
| 第一行到第三行 | 1,3                         |
| 正则表达式匹配 | sed '/^foo/q 42' input. txt |
| 反向选定    |                             |
| 步长      |                             |

### addr

1. regular expression
The following example prints all input until a line starting with thestring ‘foo’ is found.  If such line is found, ‘sed’ will terminate with exit status 42.  If such line was not found (and no other error occurred), ‘sed’ will exit with status 0.
```shell
# ‘q’ is the quit command.  ‘42’ is the command option.
sed '/^foo/q42' input.txt > output.txt
```

2. 反向选定
Appending the ‘!’ character to the end of an address specification (before the command letter) negates the sense of the match.  That is, if the ‘!’ character follows an address or an address range, then only lines which do not match the addresses will be selected.
```shell
sed '/apple/!s/hello/world/' input.txt > output.txt
sed '4,17!s/hello/world/' input.txt > output.txt
```
3. range
The following example deletes lines 30 to 35 in the input. ‘d’ is the delete command
```shell
# ‘30,35’ is an address range.
sed '30,35d' input.txt > output.txt
```
4. single line number
The following command replaces any first occurrence of ‘hello’ with ‘world’ only on line 144:
```shell
sed '144s/hello/world/' input.txt > output.txt
```
5. no address
If no address is specified, the command is performed on all lines.
```shell
sed 's/hello/world/' input.txt > output.txt
```
6. $
最后一行
7. ‘FIRST~STEP’

第一行～步长
```shell
$ seq 10 | sed -n '1~3p'
1
4
7
10
```


# 多个文件作为参数
sed 将多个输入文件看成一个长输入流。下面这个例子将打印 one. txt 的第一行和 three. txt 的最后一行。
```shell
sed -n  '1p ; $p' one.txt two.txt three.txt
```
# 使用扩展正则表达式
‘-r’
‘--regexp-extended’
 使用扩展正则表达式而不是基本正则表达式
 
 # 操作和命令
 
 ## 打印
 
p 命令
p 命令会输出原文件内容，指定的打印内容在地址后打印。
```shell
man -L us bash|sed -n '/^\w/p'
```

## 替换
```bash
sed -i 's/hello/world/g' input.txt
```
## 插入行
i 命令。在指定位置前插入一行
下面会在第一行之前插入 newline 这个词。
```bash
sed '1i newline' input.txt
```
a 命令。在指定位置后插入一行
## 插入多行
命令行里用 sed 时，单引号里的 `\n` 会被转换为换行。
sed 脚本里不需要加单引号，`\n` 也会被转换为换行。
```bash
1i2024 0331 20:43\nTags: #脚本/\n\n---\n                               
$G
$a --- 
```
## 添加空白行
G 命令
下面会将 ifile 的每一行后面加一个空白行
```bash
sed 'G' ifile
```
下面会在最后一行后加空白行
```bash
sed '$G' iflie
```

## 删除一行
```shell
‘d’  Delete the pattern space; immediately start next cycle.
```
## 单词替换
```shell
‘s/REGEXP/REPLACEMENT/[FLAGS]’
```
## 整行替换
```shell
‘c\’
‘TEXT’
     Replace (change) lines with TEXT.

‘c TEXT’
     Replace (change) lines with TEXT (alternative syntax).
```

---
