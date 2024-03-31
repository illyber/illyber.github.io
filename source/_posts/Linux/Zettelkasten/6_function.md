## 系统函数
1. basename
```shell
basename [string/pathname] [suffix]
basename 名称 [后缀]
suffix为后缀，如果suffix被指定了,basename会将pathname或string中的suffix去掉。

basename 选项... 名称...
```
2. dirname
dirname 文件绝对路径 功能描述：从给定的包含绝对路径的文件名中去除文件名（非目录的部分），然后返回剩下的路径（目录的部分）
dirname 可以理解为取文件路径的绝对路径名称
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202311250633992.png)

## 自定义函数
```shell
#方括号表示可省略
[ function ] funname[()]
{
    Action;
    [return int];
}
```
(1) 必须在调用函数地方之前，先声明函数，shell脚本是逐行运行。不会像其它语言一样先编译.
(2) 函数返回值，只能通过 $? 系统变量获得，可以显示加 :return 返回，如果不加，将以最后一条命令运行结果，作为返回值。return 后跟数值 n(0-255)