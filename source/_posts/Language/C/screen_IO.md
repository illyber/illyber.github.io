---
title: 屏幕输入输出
tags:
  - C
categories:
  - Language
  - C
---
# 缓存
- [为什么有时按两次ctrl+D才能结束标准I/O](https://blog.csdn.net/weixin_43590796/article/details/107479816#commentBox)

- 错误原因

在 Ubuntu 里运行这样一段代码：

```c
include<stdio.h>
int main(void)
{
        char ch; 
        while( (ch=getchar())!='q')
                printf("%d|", ch);
        return 0;
}
```

输入除 EOF（即<kbd>ctrl</kbd>+<kbd>d</kbd>）之外的字符时，都运行正常；输入 EOF 时，屏幕上一直打印 -1. 猜想当标准输入关闭时，一直发送 EOF.

涉及到关于输入缓冲的知识。输入缓冲分成三种：全缓冲、行缓冲、无缓冲。

​		行缓冲：收到换行符时，刷新缓冲区（换行符也被一起送去）。

总结一下：

　　回车键的效果：将缓冲区连带自身传给CPU，缓冲区清空。

　　ctrl+D（EOF）的效果：将缓冲区不带自身传给CPU，缓冲区清空。

　　缓冲区为空时收到EOF，标准文件输入关闭！

- 
- 两次

# I/O 示意图

输入输出都是站在内存角度说的

![image-20221009123241750](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281527063.png)



# 屏幕键盘 I/O
## I/O函数

目的地位置：
- fread/fwrite，getc/putc的变体（fgetc/fputc, fgets/fputs），都把文件指针放在最后
- printf/scanf的变体（fprintf/fscanf, sprintf/sscanf）都把目的地放在最前。

作用：
- fread/fwrite是二进制模式输入输出。
- get/put类的函数（getchar/putchar, fgets/fputs, gets(已废除)/puts）都是字符/字符串输入输出。文本模式。
- printf/scanf及其变体（fprintf/fscanf, sprintf/sscanf）都是格式化输出/输入。文本模式。
```c
int getchar(void);  //从stdin接收字符作为返回值输出内存
int putchar (int ch);  //输出变量ch的字符到stdin

char *gets (char *ch);
//gets()接收一行字符，即遇到换行符时停止，然后丢弃换行符，存储其余字符，并在末尾加上空字符
//在c11中，gets函数已经被废除，因为内存溢出
int puts(const char *ch);
//puts()显示字符串，并在末尾加上换行符

char *fgets( char *str, int count, FILE *stream )
//fgets()遇到换行符时停止输入，并且会接收换行符
//count表示数组元素的数量，然后把最后一个变量赋为空字符
//如果一切进行顺利，该函数返回的地址与传入的第 1 个参数相同。
//如果函数只获取了EOF没有读到任何其它内容，它将返回空指针（null pointer）。
int fputs( const char *str, FILE *stream );
//输出时不会添加换行符
//与fgets配套使用

int scanf( const char *format, ... );  //格式化字符串，变量列表（variable list）。接收一个单词（即空白处停止输入）
int printf( const char *format, ... );

int fscanf( FILE *stream, const char *format, ... )  //文件指针，格式化字符串，变量列表
int fprintf( FILE *stream, const char * ormat, ... );//可以输出到stderr

int sscanf( const char *buffer, const char *format, ... )
int sprintf( char *buffer, const char *format, ... );//按格式把数据输入字符串（字符数组）
//buffer为输入输出的对象
```
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202308031530771.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202308031532422.png)

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202308031528859.png)






## 转换说明
![image-20221013113142062](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281527064.png)

| 转换说明 | 输出                                  |
| -------- | ------------------------------------- |
| `%td`    | 以十进制输出指针之差（ptrdiff_t类型） | 

## 转换说明修饰符

```c
size_t : %zd
*: 由参数指定字段宽度。可变字段宽度。
```

![image-20221013113404923](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281527065.png)

## 输出特殊字符

```c
输出%: %%
```



# I/O 函数总结
## fread/fwrite

```c
size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *fp);
//二进制模式输出数据
//fwrite()函数返回成功写入项的数量。正常情况下，该返回值就是nmemb，但如果出现写入错误，返回值会比nmemb小。

size_t fread(void *ptr, size_t size, size_t nmemb, FILE *fp);
//二进制模式读取数据。返回读取成功的项的数量。
```

## get/put类函数（字符/字符串 I/O）

- [C语言中fgetc、fputc和getc、putc的区别是什么](https://www.cnblogs.com/bwangel23/p/4159414.html)

```c
int getchar(void);  //从stdin接收字符作为返回值输出内存
int putchar (int ch);  //输出变量ch的字符到stdin

int getc( FILE *stream );  
//从文件流stream里取一个字符到内存作为返回值
int putc( int ch , FILE *stream);  
//把变量ch里的字符输出到文件流stream
//成功时，返回被写入字符；失败时，返回 EOF 并设置 stream 上的错误指示器（见 ferror() ）。

int fgetc( FILE *stream);
//从文件流stream里取一个字符到内存作为返回值
int fputc( int ch , FILE *stream);
//把变量ch里的字符输出到文件流stream
//成功时，返回被写入字符；失败时，返回 EOF 并设置 stream 上的错误指示器（见 ferror() ）。

char *gets (char *ch);
//gets()接收一行字符，即遇到换行符时停止，然后丢弃换行符，存储其余字符，并在末尾加上空字符
//在c11中，gets函数已经被废除，因为内存溢出
int puts(const char *ch);
//puts()显示字符串，并在末尾加上换行符

char *fgets( char *str, int count, FILE *stream )
//fgets()遇到换行符时停止输入，并且会接收换行符
//count表示数组元素的数量，然后把最后一个变量赋为空字符
//如果一切进行顺利，该函数返回的地址与传入的第 1 个参数相同。
//如果函数只获取了EOF没有读到任何其它内容，它将返回空指针（null pointer）。
int fputs( const char *str, FILE *stream );
//输出时不会添加换行符
//与fgets配套使用
```

## scanf/printf类函数（格式化I/O）

```c
int scanf( const char *format, ... );  //格式化字符串，变量列表（variable list）。接收一个单词（即空白处停止输入）
int printf( const char *format, ... );

int fscanf( FILE *stream, const char *format, ... )  //文件指针，格式化字符串，变量列表
int fprintf( FILE *stream, const char * ormat, ... );//可以输出到stderr

int sscanf( const char *buffer, const char *format, ... )
int sprintf( char *buffer, const char *format, ... );
//sprintf 类似输出重定向，输出目标从屏幕改成 buffer
```

## 其它函数

以下内容在纸质书P367

```c
int ungetc(int c, FILE *fp);
int fflush(FILE *fp);

int setvbuf(FILE *fp, char *buf, int mode, size_t size);
//_IOFBF means fully buffered
//_IOLBF means line-buffered
//_IONBF means nonbuffered
//如果操作成功，函数返回0，否则返回一个非零值。

int feof(FILE *fp);
//当上一次输入调用检测到文件结尾时，feof()函数返回一个非零值，否则返回0。
int ferror(FILE *fp);
//当读或写出现错误，ferror()函数返回一个非零值，否则返回0。
```
