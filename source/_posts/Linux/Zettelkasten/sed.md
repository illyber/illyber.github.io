# sed
```shell
sed OPTIONS... [SCRIPT] [INPUTFILE...]
# script在命令行里要加单引号，在文件里不用加单引号。
sed [option] '/[regexp]/[cmd][action]'
```

sed -i 's/hello/world/g' input.txt
sed -n '/hello/p'

‘sed’ treats multiple input files as one long stream.  The following example prints the first line of the first file (‘one.txt’) and the last line of the last file (‘three.txt’).  Use ‘-s’ to reverse this behavior.
```shell
sed -n  '1p ; $p' one.txt two.txt three.txt
```
## 单引号
有歧义时加单引号
```shell
sed '1a aaa' test.list
sed 1a\aaa test.list
sed /^aaa/s/aaa/bbb/ test.list
```

## option
-n  不打印原文件
    man -L us bash|sed -n '/^\w/p'
‘-e SCRIPT’
‘--expression=SCRIPT’
     Add the commands in SCRIPT to the set of commands to be run while processing the input.

‘-f SCRIPT-FILE’
‘--file=SCRIPT-FILE’
     Add the commands contained in the file SCRIPT-FILE to the set of commands to be run while processing the input.

‘-i[SUFFIX]’
‘--in-place[=SUFFIX]’

‘-E’
‘-r’
‘--regexp-extended’
     Use extended regular expressions rather than basic regular expressions.

## script
[addr]X[options]
- ‘[addr]’ is an optional line address. ‘[addr]’ can be a single line number, a regular expression, or a range of lines.
- X is a single-letter ‘sed’ command.

### addr
1. regular expression
The following example prints all input until a line starting with thestring ‘foo’ is found.  If such line is found, ‘sed’ will terminate with exit status 42.  If such line was not found (and no other error occurred), ‘sed’ will exit with status 0.
```shell
# ‘q’ is the quit command.  ‘42’ is the command option.
sed '/^foo/q42' input.txt > output.txt
```
2. 反向选定
Appending the ‘!’ character to the end of an address specification (before the command letter) negates the sense of the match.  That is, if the ‘!’ character follows an address or an address range, then only lines which do not match the addresses will be selected.
```shell
sed '/apple/!s/hello/world/' input.txt > output.txt
sed '4,17!s/hello/world/' input.txt > output.txt
```
3. range
The following example deletes lines 30 to 35 in the input. ‘d’ is the delete command
```shell
# ‘30,35’ is an address range.
sed '30,35d' input.txt > output.txt
```
4. single line number
The following command replaces any first occurrence of ‘hello’ with ‘world’ only on line 144:
```shell
sed '144s/hello/world/' input.txt > output.txt
```
5. no address
If no address is specified, the command is performed on all lines.
```shell
sed 's/hello/world/' input.txt > output.txt
```
6. $
最后一行
7. ‘FIRST~STEP’
gawk
第一行～步长
```shell
$ seq 10 | sed -n '1~3p'
1
4
7
10
```

### commands
1. 整行删除
```shell
‘d’  Delete the pattern space; immediately start next cycle.
```
2. 替换
```shell
‘s/REGEXP/REPLACEMENT/[FLAGS]’
```
3. 整行替换
```shell
‘c\’
‘TEXT’
     Replace (change) lines with TEXT.

‘c TEXT’
     Replace (change) lines with TEXT (alternative syntax).
```
4. 追加
```shell
a TEXT
or
a\
TEXT
     Append TEXT after a line.
```
5. 插入
```shell
‘i\’
‘TEXT’
     insert TEXT before a line.

‘i TEXT’
     insert TEXT before a line (alternative syntax).
```
6. 打印文件名
```shell
‘F’
     (filename) Print the file name of the current input file (with a trailing newline).
```

7. 打印
```shell
‘p’
     Print the pattern space.
‘P’
     Print the pattern space, up to the first <newline>.
man -L us bash|sed -n '/^\w/p'
```

8. group
```shell
‘{ CMD ; CMD ... }’
     Group several commands together.
```

