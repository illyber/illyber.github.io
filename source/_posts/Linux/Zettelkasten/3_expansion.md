2024 0331 20:43
Tags: #脚本/展开

---

[shell中的扩展(Expansions)](https://opengers.github.io/linux/linux-shell-brace-parameter-command-pathname-expansion/)
## Brace Expansion（花括号）
```shell
mkdir /usr/local/src/bash/{old,new,dist,bugs}
fox@deb12  ~ ❯ echo {1..9..2} #指定步长
1 3 5 7 9
fox@deb12  ~ ❯ echo ll{1..3} 
ll1 ll2 ll3

```

## Tilde Expansion（波浪线）
## Parameter Expansion（参数）
[Shell Parameter Expansion 参数展开](https://xstarcd.github.io/wiki/shell/ShellParameterExpansion.html)

基本格式：`$parameter`或`${parameter}`, 花括号能防止误操作. 引用变量值是参数扩展的一种。
在shell中，符号`$`用作参数扩展、命令替换、算数扩展的前导符，就是说`$`符号告诉shell接下来要匹配的可能是这三种扩展中的一种。
### 参数parameter的形式

这部分我们讨论`parameter`有哪几种形式。其形式可以是变量名(例如`LANG、PWD、USER`)，数字(例如`1、2、...、n`)，特殊字符(例如`?、*、@`)，感叹号(格式:${!strings})，数组引用(例如`{num[1]}`)。具体可以查看[bash手册](https://www.gnu.org/software/bash/manual/bash.html#Shell-Parameters)

**变量名**  
变量我们很熟悉，此时`parameter`是一个变量，扩展的结果是`${parameter}`被替换为`parameter`的值。同时，如果你真的是想在屏幕输出`${LANG}`这几个字符，可以使用转义符，像这样`echo \${LANG}`

**数字**  
此时`parameter`为数字，称作位置参数，扩展的结果是`$n`被替换为命令行传入的第n个参数

**特殊字符**  
此时，`parameter`为特殊字符，此时可以不需要`{}`。特殊字符只能被引用，像这样`echo $@`，不能赋值。 `$*` 展开所有的位置参数，默认用空格分割，使用引号 特殊字符有`@、*、#、?、-、$、!、0、_`，

**感叹号**  
当`parameter`字符串第一个字符是`!`时，shell把随后的字符串解释为一个变量名，就是`${!strings}`这种形式(当然，strings要是一个正确的变量名，不能带有特殊字符)，它称作间接扩展，其特点是shell把`strings`变量的值依然看做一个变量，展开了两次。
```shell
${!parameter} # 间接展开

# 缺省值的替换
${parameter:-word} # 为空替换
${parameter:=word} # 为空替换，并将值赋给$parameter变量
${parameter:?word} # 为空报错
${parameter:+word} # 不为空替换

${#parameter}      # 获得字符串的长度

# 截取字符串，有了着四种用法就不必使用cut命令来截取字符串了。
# 在shell里面使用外部命令会降低shell的执行效率。特别是在循环的时候。
${parameter%word}  # 最小限度从后面截取word
${parameter%%word} # 最大限度从后面截取word
${parameter#word}  # 最小限度从前面截取word
${parameter##word} # 最大限度从前面截取word

${parameter/pattern/string} # 字符串替换
${parameter:offset:length}  # 截取子串

${!prefix*} # 查找参数名

其它的见man
```
### 变量内容的提取和替换/parameter expansion
参见：[caokai001 - Linux ${} 变量内容的提取和替换功能](https://www.jianshu.com/p/cbc7177cfc31)

用aa替换第一个匹配的di
```bash
[root@localhost log]# echo ${var/di/aa}

/aar1/dir2/file.txt
```
见 man bash, Parameter Expansion 条目. parameter expansion又叫variable expansion
`$par` or `${parameter}`
`${parameter#word}`
`${parameter/pattern/string}`

## Command Substitution（命令替换）
Command substitution allows the output of a command to replace the command name.
两种形式：
```shell
$(command)
`command` #backquote, 反引号
```
反引号和`$()`基本几乎等价，但尽量使用`$()`。反引号有两点不方便之处：(1)命令替换嵌套或者是包含引号的时候，反引号很麻烦，不如`$()`易读。(2)反引号处理反斜线的转义规则比较不明确，但是`$()`中的反斜线会按正常的方式转义。
## Arithmetic Expansion（算术）

形式：
```shell
let命令
#或
((expresssion)) # 在双括号里可以用算术运算符（包括+=,++等）
#或
$((expression))
```
The old format `$[expression]` is deprecated and will be removed in upcoming versions of bash.
算术运算:
```shell
a=10
b=20

val=$(( a + b))
echo "a + b : $val"
```

## Process Substitution
Process substitution allows a process's input or output to be referred to using a filename. It takes the form of
```shell
<(list) or >(list)
```

## Word Splitting
The shell scans the results of parameter expansion, command substitution, and arithmetic expansion that did not occur within double quotes for word splitting.

## Pathname Expansion（通配符）
```shell
*
?
[...]    [a-d], [:class:]
```
If the extglob shell option is enabled using the shopt builtin, the shell recognizes several extended pattern matching operators.
```shell
?(pattern-list)
Matches zero or one occurrence of the given patterns

*(pattern-list)
Matches zero or more occurrences of the given patterns

+(pattern-list)
Matches one or more occurrences of the given patterns

@(pattern-list)
Matches one of the given patterns

!(pattern-list)
Matches anything except one of the given patterns
```

## Quote Removal

---
