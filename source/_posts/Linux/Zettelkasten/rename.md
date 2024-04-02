---
title: rename
categories:
  - Linux
date: 2024-04-02 05:20
tags:
  - 基本命令/rename
---

---
# 版本
rename 有两个版本：
1. arch自带的是c语言版的。
```shell
rename foo foo00 foo?
```
2. debian 仓库里的 rename 是perl版的
```shell
rename 's/old/new/' *.old
```

# 打印操作但不执行
-n, --nono	
# 显示重命名过程
-v					

# perl 版

## 例子
将所有文件的空格替换为下划线。
要有 igm 后缀。元字符前要加反斜杠转译。
```bash
rename 's/\ /_/igm'  *
rename [选项] '命令/旧字符串匹配/新字符串/后缀' 文件名
```

## 常用命令
```shell
3.5 文件开头加入字符串(比如jelline)  
rename 's/^/jelline/' *  
3.6 文件末尾加入字符串(比如jelline)  
rename 's/$/jelline/' *

3.2 去掉文件后缀名(比如去掉.bak)  
rename 's/\.bak$//' *.bak
3.4 去掉文件名的空格  
rename 's/[ ]+//g' *

3.3 将文件名改为小写  
rename 'y/A-Z/a-z/' *
```

## 选项
```shell
1. Usage：rename [-v] [-n] [-f] perlexpr [filenames]
2. rename s/flip/flop/ *           # rename *flip* to *flop*
3. rename 's/\.flip$/.flop/' *     # rename *.flip to *.flop

4. -n(no-act)只显示将被重命名的文件，而非实际进行重命名操作
5. -v(verbose)打印被成功重命名的文件
6. -f(force)覆盖已经存在的文件
7. perlexprPerl语言格式的正则表达式
8. files需要被替换的文件(比如*.c、*.h)，如果没给出文件名，将从标准输入读
```
## 命令
- 三种形式
	- 匹配：m/ /  (可以省略m，直接写成/regexp/)
	- 替换：s/ / / 
	- 转化：tr/ / /
## 匹配
- perlexpr 结尾必须加斜杠封闭
## 后缀
- 斜杠后加g表示全部替换



---
