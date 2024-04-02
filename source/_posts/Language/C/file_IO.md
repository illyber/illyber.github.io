---
title: 文件操作
tags:
  - C
categories:
  - Language
---
# 文本文件与二进制文件的区别

- 文本文件：以字符编码形式存储到磁盘文件
- 二进制文件：将内存数据原样存储到磁盘文件
- 二进制模式：模式字符串加b

eg: 浮点数以文本模式输出到文件后，就成为了字符串

# 换行与文件结尾

| 系统           | 换行                                                         | 结尾                                                         |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| UNIX/Linux     | \n (换行符)                                                  | 记录文件大小，计数确认是否读到结尾                           |
| OS X Macintosh | \r (回车符)                                                  |                                                              |
| MS-DOS         | \r\n                                                         | Ctrl+z                                                       |
| Windows        | Notepad 生成 MS-DOS 格式的文件，新的编辑器生成类 UNIX 格式的文件 | Notepad 生成 MS-DOS 格式的文件，新的编辑器生成类 UNIX 格式的文件 |

两种访问模式，**文本模式**和**二进制模式**：

1. 文本模式：把本地系统的格式转换成 C 的格式，比如在 MS-DOS 系统上把 \r\n 转换成 \n；
2. 二进制模式：在二进制模式，程序能访问文件的每一个字节；文件格式不会被转换；

UNIX 用同一种格式处理文本文件和二进制文件，所以**这两种模式对 UNIX 相同**。

getc() 读到结尾返回EOF。**程序一定会读到超过文件末尾。**


# fopen() 和 fclose()

- 文本模式：将内存里的位组合转化为**字符编码**。

- 二进制模式：按内存里的位组合写入到文件；

fopen() 和 fclose()

```c
fopen("filename", mode);
fclose(FILE *);
```

# fopen()的模式字符串

![image-20220510235440367](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281527066.png)

| 模式字符串 | 含义、能否控制读写开始的位置                                 |
| ---------- | ------------------------------------------------------------ |
| "r"        | 只能读                                                       |
| "w"        | 只能重新写                                                   |
| "a"        | 只能在末尾添加                                               |
| "r+"       | 最自由的模式。从文件指针的位置开始读写。                     |
| "w+"       | 从文件指针位置开始读；写时会先把所有文件数据抹掉重新写。先抹再写。 |
| "a+"       | 从文件指针位置开始读；不能控制写开始的位置，只能在末尾添加   |

文件指针与数组类似，偏移量像下标。至少文本文件有 EOF。

# fseek() 和 ftell()

```c
int fseek (FILE *, long int offset, int starting_point);
//形参：文件指针、偏移量、模式
//偏移量:向左为负，向右为正；在数字后加L后缀
//模式：SEEK_SET（文件开头）, SEEK_CUR（当前位置）, SEEK_END（文件末尾，即EOF）.

long int ftell(FILE *stream);
//当前位置-文件起点。当前位置到文件开头的字节数。
```
# fgetpos()和fsetpos()

适用于大文件。fseek()和ftell()适用于long大小的文件。

# rewind

# 文件指针是怎么移动的？

![IMG_0835](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281527068.png)



# 文件I/O 函数

**目的地位置：**
- fread/fwrite，getc/putc的变体（fgetc/fputc, fgets/fputs），都把文件指针放在最后
- printf/scanf的变体（fprintf/fscanf, sprintf/sscanf）都把目的地放在最前。

**作用：**
- fread/fwrite是二进制模式输入输出。
- get/put类的函数（getchar/putchar, fgets/fputs, gets(已废除)/puts）都是字符/字符串输入输出。文本模式。
- printf/scanf及其变体（fprintf/fscanf, sprintf/sscanf）都是格式化输出/输入。文本模式。

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
file, string
```c
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
