2024 0331 16:37
Tags: #脚本/例子

---
<!-- toc -->
shell脚本实质是一系列命令。空格 token split.
# 0.执行脚本的方式
1. bash或sh+脚本的相对路径或绝对路径（不用赋予脚本+x权限）.子shell中运行
2. 输入脚本的绝对路径或相对路径执行脚本（必须具有可执行权限+X）.子shell中运行
3. 在脚本的路径前加上“.”或者source. "."是个命令，bash中用. 当前shell中运行

# 1.逐行读取文件
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


# 2.重命名脚本

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







---
