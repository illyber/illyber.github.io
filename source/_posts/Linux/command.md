---
title: shell-command
tags:
  - linux
  - shell
categories:
  - Shell
date: 2023-11-17
updated:
---

<!-- toc -->

# awk
AWK的几个实现：
1. AWK:原先来源于AT&T实验室的的AWK; AT&T(American Telephone & Telegraph的缩写 是一家美国电信公司)
2. NAWK:AT&T实验室的AWK的升级版;
3. GAWK:这就是GNU AWK；
4. MAWK:一种轻巧快速的AWK实现。

[简单教程 - Awk 基础教程](https://www.twle.cn/c/yufei/awk/awk-basic-index.html)

AWK 主体代码有着如下的语法
```shell
awk '/pattern/ {awk-commands}' filename
awk '/术/ {print $0}' employee.txt
```

每行按空格或 tab 分割
```shell
# 输出包含 "compiler" 的行
awk '/compiler/ ' log.txt

# 输出第二列
awk '{print $2}' log.txt

# 打印最后一列
awk '{print $NF}' log.txt
# 如果在命令表达式中使用没有$符号的NF变量，这个变量将显示一行记录中有多少个字段。
# 如果使用带有$符号的NF变量，这个变量将显示一行记录中最后一个字段。
# Number of Field

```

eg
```shell
[www.twle.cn]$ awk 'BEGIN{printf "序号\t名字\t部门\t年龄\n----------------------------\n"}{print}END{printf "----------------------------\n"}' employee.txt
```

编辑目录，将页码减去三十，tab 为分隔符，输出到 result.txt
```shell
awk -F "\t"  '{$NF=$NF-30;print}' outline-bk.txt|less > result.txt
```

# sed
```shell
sed OPTIONS... [SCRIPT] [INPUTFILE...]
sed [option] '/[regexp]/[cmd][action]'
```
script在命令行里要加单引号，在文件里不用加单引号。
sed -i 's/hello/world/g' input.txt
sed -n '/hello/p'

‘sed’ treats multiple input files as one long stream.  The following example prints the first line of the first file (‘one.txt’) and the last line of the last file (‘three.txt’).  Use ‘-s’ to reverse this behavior.
```shell
sed -n  '1p ; $p' one.txt two.txt three.txt
```
## 单引号
有歧义时加单引号
```shell
sed '1a aaa' test.list
sed 1a\aaa test.list
sed /^aaa/s/aaa/bbb/ test.list
```

## option
-n  不打印原文件
    man -L us bash|sed -n '/^\w/p'
‘-e SCRIPT’
‘--expression=SCRIPT’
     Add the commands in SCRIPT to the set of commands to be run while processing the input.

‘-f SCRIPT-FILE’
‘--file=SCRIPT-FILE’
     Add the commands contained in the file SCRIPT-FILE to the set of commands to be run while processing the input.

‘-i[SUFFIX]’
‘--in-place[=SUFFIX]’

‘-E’
‘-r’
‘--regexp-extended’
     Use extended regular expressions rather than basic regular expressions.

## script
[addr]X[options]
- ‘[addr]’ is an optional line address. ‘[addr]’ can be a single line number, a regular expression, or a range of lines.
- X is a single-letter ‘sed’ command.

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
gawk
第一行～步长
```shell
$ seq 10 | sed -n '1~3p'
1
4
7
10
```

### commands
1. 整行删除
```shell
‘d’  Delete the pattern space; immediately start next cycle.
```
2. 替换
```shell
‘s/REGEXP/REPLACEMENT/[FLAGS]’
```
3. 整行替换
```shell
‘c\’
‘TEXT’
     Replace (change) lines with TEXT.

‘c TEXT’
     Replace (change) lines with TEXT (alternative syntax).
```
4. 追加
```shell
a TEXT
or
a\
TEXT
     Append TEXT after a line.
```
5. 插入
```shell
‘i\’
‘TEXT’
     insert TEXT before a line.

‘i TEXT’
     insert TEXT before a line (alternative syntax).
```
6. 打印文件名
```shell
‘F’
     (filename) Print the file name of the current input file (with a trailing newline).
```

7. 打印
```shell
‘p’
     Print the pattern space.
‘P’
     Print the pattern space, up to the first <newline>.
man -L us bash|sed -n '/^\w/p'
```

8. group
```shell
‘{ CMD ; CMD ... }’
     Group several commands together.
```

# column 命令
可以将文本结果转换为整齐的表格，上下对齐
```shell
cat /etc/passwd|sort -t ":" -nk 3|column -s ":" -t
```
`-s`: 指定分隔符
`-t`: 以表格形式输出（没有线）

# find
更多参见：[菜鸟教程 - Linux find 命令](https://www.runoob.com/linux/linux-comm-find.html)
查找当前目录下名为 file.txt 的文件：
```shell
find . -name file.txt
```

将当前目录及其子目录下所有文件后缀为 .c 的文件列出来:
```shell
find . -name "*.c"
```

将当前目录及其子目录中的所有文件列出：
```shell
find . -type f
```

查找 /home 目录下大于 1MB 的文件：
```shell
find /home -size +1M
```

# xargs
$()
分隔符`-d`与执行次数`-n`
[每天一个Linux命令-xargs](https://www.bilibili.com/video/BV1q8411R7tw/?spm_id_from=333.880.my_history.page.click&vd_source=4f8ddad44fd904574089cafb91e9e009)

# info

1. 安装pinfo, pinfo有颜色：`sudo apt install pinfo`
2. 快捷键：
    - p 前一个节点
    - n 后一个节点
    - u 上一层节点
    - j,k 光标上移下移
    - b 或 t 或 Home    文档的开始（b 是 begining 的意思）
    - e 或 End          文档的末尾（b 是 ending 的意思）
    - SPACE键 向前滚动一页。 
    - BACKUP或DEL键 向后滚动一页。
    ![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202311262234813.png)

# grep

grep pattern file
-i 忽略大小写
-w 匹配整个单词
-e 查找多个字符串。grep -e pattern1 -e pattern2 file
-n 打印目标的行数
-v 打印不符合模式的行
-r 递归查找文件，用于目录
-l 打印包含模式的文件名
-E, --extended-regexp 启用扩展正则表达式

# cat

-n	打印所有行号
-b	打印非空行行号
-s	多个空行合并成一个空行
-E	每行末尾加一个 $ 符号
-T	打印制表符
-A	同时实现 -E 和 -T

cat 可以同时查看多个文件

# find

- 在 `/home/carryf` 里搜索 `"cdr_*.conf"` ,并且排除 `/home/carryf/astetc` 目录

```shell
find /home/carryf -path "/home/carryf/astetc" -prune -o -type f -name "cdr_*.conf" -print
```













