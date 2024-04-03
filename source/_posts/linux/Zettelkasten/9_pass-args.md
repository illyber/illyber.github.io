---
title: 9_pass-args
date: 2024-04-02 05:20
tags:
  - 脚本/传递参数
categories:
  - Linux
---

---

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



---
