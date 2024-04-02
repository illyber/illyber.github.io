---
title: 8_control-flow
categories:
  - Linux
date: 2024-04-02 05:20
tags:
  - 脚本/控制流
---

---

# if 判断

双小括号里用数值比较式
```shell
if (($a > 2))
```

方括号里用非数值比较式。方括号和内容之间要有空格。
[[5_operator#文件测试运算符]]
```bash
if [ 条件判断式 ]
then
	程序
fi
```

(1)单分支

不换行就用分号代替换行符

```shell
if [ 条件判断式 ];then
	程序
fi
或者
if [ 条件判断式 ]
then
	程序
fi
```

(2)多分支

```shell
if [ 条件判断式 ]
then
	程序
elif [ 条件判断式 ]
then
	程序
else
	程序
fi
```

(3)结合多条件判断

```shell
if [ ] && [ ]
或
if [ 表达式1 -a 表达式2 ]
```

# case语句

```shell
case $变量名 in
值1)
	如果变量的值等于值1，则执行程序1
;;
值2)
	如果变最的值等于值2，则执行程序2
;;
	...省略其他分支...
*)
	如果变量的值都不是以上的值，则执行此程序
;;
esac
```

注意事项:
(1)case行尾必须为单词“in”，每一个模式匹配必须以右括号“)”结束。
(2)双分号“;;”表示命令序列结束，相当于c中的break
(3)最后的“`*)`”表示默认模式，相当于c中的default。

# for循环变量取值

现在一般都使用for in结构，for in结构后面可以使用函数来构造范围，比如$()、\`\`这些，里面写一些查找的语法，比如ls test\*，那么遍历之后就是输出文件名了。

## 结构
命令行里有分号
```bash
for file in $(ls *md);do echo $file;done
```

脚本里不需要分号，但需要换行
```bash
for file in $(ls *md)
do echo $file
done
```

## 第一类：遍历文件

```shell
for file in /proc/*;  

for file in $(ls *.sh)

for file in $(echo [0-9]*_*md);do sed -f sed_script $file -i;done

for i in `ls`;  

for i in $* ;
# 注意与$@的区别，但是不加双引号时一样
```

## 第二类：遍历字符串组

Shell 脚本中有个变量叫 IFS (Internal Field Seprator) ，内部域分隔符。完整定义是 The shell uses the value stored in IFS, which is the space, tab, and newline characters by default, to delimit words for the read and set commands, when parsing output from command substitution, and when performing variable substitution.
Shell 的环境变量分为 set, env 两种，其中 set 变量可以通过 export 工具导入到 env 变量中。其中，set 是显示设置 shell 变量，仅在本 shell 中有效；env 是显示设置用户环境变量 ，仅在当前会话中有效。换句话说，set 变量里包含了 env 变量，但 set 变量不一定都是 env 变量。这两种变量不同之处在于变量的作用域不同。显然，env 变量的作用域要大些，它可以在 subshell 中使用。
IFS 是一种 set 变量，当 shell 处理"命令替换"和"参数替换"时，shell 根据 IFS 的值，默认是 space, tab, newline 来拆解读入的变量，然后对特殊字符进行处理，最后重新组合赋值给该变量。

笼统的说，bash实现字符串遍历的方式，实际是定义一个数组然后遍历其元素

### 示例 1：字符串组不加双引号，空格分隔
```shell
这里的字符串不用加引号
# Read a string with spaces using for loop
for value in I like programming
do
    echo $value
done
```
输出
```
I
like
programming
```

### 示例 2：字符串组加引号，用 $引用
在变量 StringVal 中分配文本，并使用 for 循环读取此变量的值。
```bash
# Define a string variable with a value
StringVal="Welcome to linuxhint"

# Iterate the string variable using for loop
for val in $StringVal
do
    echo $val
done
```
bash 的输出（用双引号内的空格分隔）
```
Welcome
to
linuxhint
```
zsh 的输出（不用双引号内的空格分隔）
```
Welcome to linuxhint
```

### 示例 3：declare
在此脚本中使用类型声明字符串值的数组。数组中包含空格的两个值是“ Linux Mint”和“ Red Hat Linux”。该脚本将这些值拆分为多个单词并将其打印为单独的值，从而生成输出。但这不是正确的输出。下一个示例显示了此类问题的解决方案。
```bash
# Declare an array of string with type
declare -a StringArray=("Linux Mint" "Fedora" "Red Hat Linux" "Ubuntu" "Debian" )
 
# Iterate the string array using for loop
for val in ${StringArray[@]}; do
   echo $val
done
```
输出结果
```bash
Linux
Mint
Fedora
Red
Hat
Linux
Ubuntu
Debian
```
### 示例 4：declare
```bash
# Declare a string array with type
declare -a StringArray=("Windows XP" "Windows 10" "Windows ME" "Windows 8.1"
"Windows Server 2016" )
 
# Read the array values with space
for val in "${StringArray[@]}"; do
  echo $val
done
```
输出结果
```bash
Windows XP
Windows 10
Windows ME
Windows 8.1
Windows Server 2016
```

### 示例 5：星号遍历字符串数组
```bash
#Declare a string array
LanguageArray=("PHP"  "Java"  "C#"  "C++"  "VB.Net"  "Python"  "Perl")
 
# Print array values in new lines
echo "Print every element in new line"
for val1 in ${LanguageArray[*]}; do
     echo $val1
done
 
echo ""
 
# Print array values in one line
echo "Print all elements in a single line"
for val2 in "${LanguageArray[*]}"; do
    echo $val2
done
echo ""
```
输出结果
```bash
Print every element in new line
PHP
Java
C#
C++
VB.Net
Python
Perl

Print all elements in a single line
PHP Java C# C++ VB.Net Python Perl
```
### 示例 6：指定逗号为 IFS
在这里，逗号（，）用于分割字符串值。 IFS 变量用于设置字段分隔符。
```bash
DataList=" HTML5, CCS3, BootStrap, JQuery "
Field_Separator=$IFS
 
# set comma as internal field separator for the string list
IFS=,
for val in $DataList;
do
echo $val
done
 
IFS=$Field_Separator
```
输出结果
```bash
HTML5
CCS3
BootStrap
JQuery
```
### 示例 7：合并字符串数组
示例演示怎么合并多个数据并遍历出来
```bash
str_array1=("Magento 2.2.4" "WooCommerce")
str_array2=("CodeIgnitor" "Laravel")
combine=(str_array1 str_array2)
for arrItem in ${combine[@]}
do
   eval 'for val in "${'$arrItem'[@]}";do echo "$val";done'
done
```
输出结果
```
Magento 2.2.4
WooCommerce
CodeIgnitor
Laravel
```

### 示例 8：使用模式读取字符串列表
在这里，“ /，/”模式用于根据逗号分割字符串值。
```bash
# Define a list of string variable
stringList=WordPress,Joomla,Magento
 
# Use comma as separator and apply as pattern
for val in ${stringList//,/ }
do
   echo $val
done
```
输出结果
```
WordPress
Joomla
Magento
```

### 示例 9：用@符号
```bash
arr=("0" "1" "2" "3" "4" "5" "6" "7" "8" "9" "a" "b" "c" "e" "e" "f")
 
for value in ${arr[@]}
do
  echo $value
done


# 或者采取如下方式
for (( i = 0 ; i < ${#arr[@]} ; i++ ))
do
  echo ${arr[$i]}
done
```



## 第三类：计数循环/变量取值为数字

双小括号里用可以用数值
```shell
for i in {1..10} 

for((i=1;i<=10;i++))
do awk 'BEGIN{for(i=1; i<=10; i++) print i}'
done

for i in $(seq 1 10)
do echo $i
done
```
seq 命令
用法：seq [选项]... 尾数
　或：seq [选项]... 首数 尾数
　或：seq [选项]... 首数 增量 尾数
打印从 <首数> 到 <尾数> 的数字，且每两个数字间的步长为 <增量>。
如果省略了 <首数> 或者 <增量>，则默认值为 1。


# while 循环

```shell
while [ 条件判断式 ]
do
	程序
done
```


---
