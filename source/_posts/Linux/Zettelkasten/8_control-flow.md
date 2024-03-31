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
(3)最后的“`*)`”表示默认模式，相当于c中的default。

## for循环

现在一般都使用for in结构，for in结构后面可以使用函数来构造范围，比如$()、\`\`这些，里面写一些查找的语法，比如ls test\*，那么遍历之后就是输出文件名了。

在双小括号里可以用关系符号（如大于号小于号）

```shell
if (($a > 2))
```

### 第一类：数字性循环

```shell
for i in {1..10} 

for i in $(seq 1 10) 

for((i=1;i<=10;i++));  
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

### 第三类：文件名查找

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

