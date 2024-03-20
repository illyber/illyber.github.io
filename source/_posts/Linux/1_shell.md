---
title: Shell-脚本编程
tags:
  - shell
categories:
  - Shell
---

<!-- toc -->
shell脚本实质是一系列命令。空格 token split.
# 逐行读取文件
- 用awk
```shell
cat myfile |awk '{print "Line contents are: "$0}' 
```
- 管道
```shell
cat myfile |
while read rows 
do
 echo "$rows"
done
```
- 输入重定向
```shell
while read rows 
do
 echo "$rows"
done < myfile           
```


# shell例子 - 重命名脚本

变量定义 `h="hello"`
变量引用 `$h`
变量可连接 `echo "abc$hxyz"`
防止变量歧义 `"abc${h}xyz"`

重命名 week->chapter
井号掐头，百分号去尾
```shell
for ff in week??
do
echo $ff
done

for ff in week??
do
echo ${ff#week} #掐头
done

for ff in week??
do
echo chapter${ff#week}
done

for ff in week??
do
echo " mv $ff chapter${ff#week}"
done

for ff in week??
do
mv $ff chapter${ff#week}
done
```

# 执行脚本的方式
1. bash或sh+脚本的相对路径或绝对路径（不用赋予脚本+x权限）.子shell中运行
2. 输入脚本的绝对路径或相对路径执行脚本（必须具有可执行权限+X）.子shell中运行
3. 在脚本的路径前加上“.”或者source. "."是个命令，bash中用. 当前shell中运行


# 流程控制

## if 判断

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

## case语句

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
(3)最后的“*)”表示默认模式，相当于c中的default。

## for循环

在双小括号里可以用数学符号（如大于号小于号）

```shell
if (($a > 2))
```

### 第一类：数字性循环

```shell
for((i=1;i<=10;i++));  

for i in $(seq 1 10)  

for i in {1..10}  

awk 'BEGIN{for(i=1; i<=10; i++) print i}'  
```

### 第二类：字符性循环

```shell
for i in `ls`;  

for i in $* ;
# 注意与$@的区别，但是不加双引号时一样

for i in f1 f2 f3 ;  

list="rootfs usr data data2"  
for i in $list;  
```

### 第三类：路径查找

```shell
for file in /proc/*;  

for file in $(ls *.sh)
```

## while 循环

```shell
while [ 条件判断式 ]
do
	程序
done
```



# read 读取控制台输入
read (选项) (参数)
1)选项:
-p: 指定读取值时的提示
-t: 指定读取值时等待的时间（秒）如果-t不加表示一直等待
2)参数
变量: 指定读取值的变量名
```shell
#!/bin/bash
read -t 7 -p "Enter your name in 7 seconds :" NN
echo $NN
```

# 参数传递
## 总结
[提莫的蘑菇 - xargs 命令--Shell管道传递参数](https://zhuanlan.zhihu.com/p/157758410)
```shell
管道      将上一个的标准输出转化为下一个的标准输入

xargs    将标准输入转为命令行输入参数，与$()相似
    "echo "one two three" | xargs mkdir" == "mkdir one two three"

$()      命令替换，将包裹的命令输出作为参数，比``好

``       反引号，将包裹的命令输出作为参数

$0, $1, $2    命令行参数。$0 是程序名

重定向 >

-	代表标准输入
```
## xargs
$()
分隔符`-d`与执行次数`-n`
[每天一个Linux命令-xargs](https://www.bilibili.com/video/BV1q8411R7tw/?spm_id_from=333.880.my_history.page.click&vd_source=4f8ddad44fd904574089cafb91e9e009)

