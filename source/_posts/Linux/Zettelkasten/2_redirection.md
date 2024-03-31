# 例子程序
>[!example]
>向stdout输出
>```c
>#include<stdio.h>
>//output.c
>int main()
>{
 >   char str[100]="army";                      
 >   printf("stdout:%s\n",str);
  >  return 0;
>}
>```



>[!example]
>向stderr输出
```c
#include<stdio.h>
//error.c
int main()
{
    char str[100]="army";
    fprintf(stderr,"stderr:%s\n",str);                      
    return 0;
}
```

>[!example]
>从stdin输入，向stdout和stderr输出
```c
#include<stdio.h>
//mytext.c
int main()
{
    char str[100];                     
    scanf("%s",str);
    printf("stdout:%s\n",str);
    fprintf(stderr,"stderr:%s\n",str);
    return 0;
}
```


# 重定向/Redirection
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/20240321013029.png)

## 输出重定向
>[!definition]
>[n]>filename
>[n]>>filename

将文件描述符n指向filename，filename以可写方式打开。
`>`	从filename头写起
`>>`	在filename后追加
方括号不用写。方括号表示可以省略，如果不写数字，默认n=1. 

未重定向时

n=1时，标准输出到filename
n=2时，标准错误输出到filename


>[!example]
>几个例子

```bash
./output > ifile && less ifile
./output 2> ifile && less ifile
./error > ifile && less ifile
./error 2> ifile && less ifile
```

## stdout/stderr 同时重定向
>[!definition]
>`&> word`
>`>& word`

将标准输出与标准错误输出都定向到word代表的文件（以写的方式打开），两种格式意义完全相同，这种格式完全等价于 > word 2>&1 (2>&1 是将标准错误输出复制到标准输出，&是为了区分文件1和文件描述符1的，详细的介绍后面会有)
例如: `mkdir &> file` mkdir报错，由于标准错误被重定向到file文件，可以在file中看到报错内容

### 同时将标准输出和标准错误输出到dirlist.
```bash
ls &> dirlist
ls >& dirlist
ls >  dirlist 2>&1
```

### 只将标准输出输出到dirlist
```bash
ls 2>&1 > dirlist
#让2指向了1所指向的，也就是stdout
```
原理：
1. 解析 `2>&1` 后
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/20240321011242.png)
2. 再解析 `>` 后
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/20240321011431.png)
所以只输出标准输出到file




同时追加重定向标准输出和标准错误:
```shell
&>>word
>>&word
>>word 2>&1
```


## 输入重定向
>[!definition]
>`[n]<filename`
>`[n]<<filename`

说明：将文件描述符 n 重定向到 filename 指代的文件（以只读方式打开）,如果n省略就是0（标准输入）
例如：`cat 0<file`或者`cat<file`代表输入重定向到file文件，用cat查看时，从标准输入读取内容，也就是读取了file文件内容

如果不写数字，默认n=0. n=0时。


cat命令也在输入重定向中有用
```
没有指定文件时，cat将标准输入直接转化为标准输出
    cat << EOF
```

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202311271814728.png)

## 组合

cat < test.list >  new.list
新建文件： cat > test.txt << EOF

## 复制标识符
>[!definition]
>`[n]<&[m]`
>`[n]>&[m]`

这里两个都是将文件描述符 n 复制到 m ，两者的区别是，前者是以只读的形式打开，后者是以写的形式打开 因此 0<&1 和 0>&1 是完全等价的（读/写方式打开对其没有任何影响） 这里的& 目的是为了区分数字名字的文件和文件描述符，如果没有& 系统会认为是将文件描述符重定向到了一个数字作为文件名的文件，而不是一个文件描述符
shell先解析再执行

# 文件标识符
相当于C语言的指针

| 标识符 | 对应文件   |
| :-: | ------ |
|  0  | stdin  |
|  1  | stdout |
|  2  | stderr |


