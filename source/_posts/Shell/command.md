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

[简单教程 - Awk 基础教程](https://www.twle.cn/c/yufei/awk/awk-basic-index.html)

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

AWK 主体代码有着如下的语法
```shell
awk '/pattern/ {awk-commands}' filename
awk '/术/ {print $0}' employee.txt
```

eg
```shell
[www.twle.cn]$ awk 'BEGIN{printf "序号\t名字\t部门\t年龄\n----------------------------\n"}{print}END{printf "----------------------------\n"}' employee.txt
```

编辑目录，将页码减去三十，tab 为分隔符，输出到 result.txt
```shell
awk -F "\t"  '{$NF=$NF-30;print}' outline-bk.txt|less > result.txt
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