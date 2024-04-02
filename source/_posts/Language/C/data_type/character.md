---
title: 字符
tags:
  - C
categories:
  - Language
---
# 字符/字符变量

**转义序列**

- 转义字符：C语言中，转义字符是斜杠`\`；能将转义字符和后面的东西替换成其它字符
- 转义序列（escape sequence）：如`\n`，8进制转义序列`\101`，16进制转义序列`\x41`；是转义字符和后面的字符组成的序列
- 控制字符：用于「控制」的字符。
- 非打印字符：无法显示出来的字符

**diff:**  

1. 转义字符只有一个字符，转义序列是多个字符组成的序列。  
2. 非打印字符包含控制字符  
3. 换行符LF的转义序列是`\n`

**CTRL+字母：**

1. ASCII码1，2，3…分别依次对应键盘按键的`Ctrl+A`键，`Ctrl+B`键，`Ctrl+C`键，…`Ctrl+Z`键的ASCII为26.  
2. 参考大写字母后的编码，按键`Ctrl+[`键产生ASCII码27，`Ctrl+\`键产生ASCII码28，`Ctrl+]`键产生ASCII码29，`Ctrl+^`键产生ASCII码30。

[键盘各键对应的编码值（key code）](https://tangyilong.com/2019/04/13/%E5%AD%97%E6%AF%8D%E5%AF%B9%E5%BA%94%E7%9A%84ASCII%E7%A0%81%E5%92%8CCTRL%E5%8A%A0%E5%AD%97%E6%AF%8D%E7%9A%84/)



# 字符函数

![image-20220430225753570](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281527060.png)

![image-20220430225821521](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281527061.png)

11.9 字符串数字转数值数字的函数

| 函数      | 作用                                                    | 例子                          |
| --------- | ------------------------------------------------------- | ----------------------------- |
| atoi()    | 字符串数字转数值数字                                    | atoi("42regular")将返回整数42 |
| atol()    | 把字符串转换成long类型的值                              |                               |
| atof()    | 把字符串转换成 double 类型的值                          |                               |
| strtol()  | 把字符串转换成long类型的值，可以指定数字的进制          |                               |
|           | `(char *nptr, char **endptr, int base)`                 |                               |
| strtoul() | 把字符串转换成unsigned long类型的值，可以指定数字的进制 |                               |
| strtod()  | 把字符串转换成double类型的值                            |                               |

