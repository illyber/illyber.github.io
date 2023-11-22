---
title: Linux 文件和目录
tags:
  - linux
categories:
  - Linux
date: updated
---
# [Linux各文件颜色的含义](https://www.cnblogs.com/zouhong/p/12154352.html)

Linux系统中文件有多种颜色，不同颜色文件代表不同类型的文件，具体如下：

- **蓝色**：目录   
- **绿色**：可执行文件
- **红色**：压缩文件
- **浅蓝色**：链接文件
- 白色：普通文件
- **黄色**：设备文件

# 各目录的作用
常见的目录名均基于文件系统层级标准（filesystem hierarchy standard，FHS），官网：
http://www.pathname.com/fhs。
![](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281946409.png)

# 设置用户目录下默认文件夹

先把当前用户名添加到 sudoers files，再设置

```shell
cd ~
mkdir Desktop Download Templates Public Documents Music Pictures Videos
rm -rf 公共 模板 视频 图片 文档 下载 音乐 桌面
xdg-user-dirs-update --set DESKTOP ~/Desktop
xdg-user-dirs-update --set DOWNLOAD ~/Download
xdg-user-dirs-update --set TEMPLATES ~/Templates
xdg-user-dirs-update --set PUBLICSHARE ~/Public
xdg-user-dirs-update --set DOCUMENTS ~/Documents
xdg-user-dirs-update --set MUSIC ~/Music
xdg-user-dirs-update --set PICTURES ~/Pictures
xdg-user-dirs-update --set VIDEOS ~/Videos
```

重启后重命名生效

xdg支持以下关键字对应默认的目录，见 `man xdg-user-dirs-update`

```shell
DESKTOP
DOWNLOAD
TEMPLATES
PUBLICSHARE
DOCUMENTS
MUSIC
PICTURES
VIDEOS
```

用以下命令设置

```shell
xdg-user-dirs-update --set DESKTOP /home/你的用户名/desktop
```

相关配置项存在于 `/etc/xdg/user-dirs.conf` 和 `~/.config/user-dirs.dirs`

xdg 指 X Desktop Group - X 桌面组，是一套标准，现在改名为 freedesktop，但是一些软件包、文件还是保持 xdg 的名字。

# 删除/重命名文件

|                 |                                                                                                   | 命令                     |
| --------------- | ------------------------------------------------------------------------------------------------- | ------------------------ |
| 删除文件        | 删除 filename 之外的文件                                                                          | rm !(filename)           |
|                 | 删除 C 源代码以外的文件（可能需要设置bash zsh）                                                   | `rm -v !(*c)`            |
| 删除目录        | 删除 directory                                                                                    | rm -r directory          |
| 重命名文件/目录 | 将所有文件的空格替换为下划线<br />要有 igm 后缀！<br />元字符前要加反斜杠转译！<br />可不加单引号 | `rename 's/\ /_/igm'  *` |
| tree            | 树形列出目录                                                                                      | tree -L 2                |
# rename命令
rename 有两个版本. arch自带的是c语言版的
```shell
rename [options] expression replacement file...
#eg:
rename foo foo00 foo?
```
另一种是perl版的
```shell
rename 's/old/new/' *.old
```

perl-rename 命令
在 `.zshrc` 里设置了 `alias rename = 'perl-name'`

采用正则表达式。

选项
```shell
1. Usage：rename [-v] [-n] [-f] perlexpr [filenames]
2. rename s/flip/flop/ *           # rename *flip* to *flop*
3. rename 's/\.flip$/.flop/' *     # rename *.flip to *.flop

4. -n(no-act)只显示将被重命名的文件，而非实际进行重命名操作
5. -v(verbose)打印被成功重命名的文件
6. -f(force)覆盖已经存在的文件
7. perlexprPerl语言格式的正则表达式
8. files需要被替换的文件(比如*.c、*.h)，如果没给出文件名，将从标准输入读
```

- 三种形式
	- 匹配：m//  (可以省略m，直接写成/regexp/)
	- 替换：s/// 
	- 转化：tr///　
- perlexpr 结尾必须加斜杠封闭
- 斜杠后加g表示全部替换
- 常用命令
```shell
3.5 文件开头加入字符串(比如jelline)  
rename 's/^/jelline/' *  
3.6 文件末尾加入字符串(比如jelline)  
rename 's/$/jelline/' *

3.2 去掉文件后缀名(比如去掉.bak)  
rename 's/\.bak$//' *.bak
3.4 去掉文件名的空格  
rename 's/[ ]+//g' *

3.3 将文件名改为小写  
rename 'y/A-Z/a-z/' *
```

# 复制文件

- 复制多个文件到指定目录：

```shell
cp <dir>/file1 <dir>/file2 <dir>/file3  <target_dir>
# 也可以向下面这样简写：
cp <dir>/{file1,file2,file3} <target_dir>
# 将dir目录里的 file1, file2, file3 复制到 target_dir
```


[tar、7z（7zip）压缩/解压缩指令的使用](http://www.javashuo.com/article/p-drffcegm-go.html)

# tar 命令

## 打包/解包/列出

```bash
打包、解包 Examples:
  tar -cf archive.tar foo bar  # creat, file（使用档案名）. 创建归档.
  tar -tvf archive.tar         # list, verbose, file. 列出压缩包内容.
  tar -xf archive.tar          # extract, file. 解包归档.
  -v, --verbose                # verbose 详细地列出处理的文件
  -f,                          # file 使用归档名字，切记，这个参数是最后一个参数，后面只能接归档名。（必须加此参数）
```

## 压缩/解压

压缩选项。解压时不必制定压缩格式，tar 会自动识别。

| 压缩选项            | 含义                                                         |
| ------------------- | ------------------------------------------------------------ |
| -a, --auto-compress | 使用归档后缀名来决定压缩程序                                 |
| -z                  | 用 gzip（gnu zip，即 gnu 版 zip） 压缩，后缀为 .gz；         |
| -j                  | 用 bzip2 压缩，后缀为 .bz2；                                 |
| -J, --xz            | 用 LZMA 算法压缩，后缀为 .xz；压缩率最高但有点慢             |
| -f                  | 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名。（必须加此参数） |

```bash
多线程压缩
tar --use-compress-program=pigz -cpvf linux-5.19.tar.gz linux-5.19/ # 要先安装pigz（parallel implementation of gzip）

tar -cvf - dir1 dir2 dir3 | zstd -T0  > output.tar.zst
# zstd没有压缩文件夹的选项，只能压缩单个文件。若想压缩文件夹，可以结合tar使用
```

## 其它选项

|                                     要求                                      |                           命令                           |
|:-----------------------------------------------------------------------------:|:--------------------------------------------------------:|
|                                解压到指定目录                                 |                            -C                            |
|                                                                               |      tar -xf archive.tar.xz -C /home/linuxize/files      |
|                                 解压指定文件                                  |          tar -zxvf /root/etc.tar.gz etc/shadow           |
|            解压指定文件（-T）到指定目录（-C）.-T 一定要在 -C 之后             |     tar -xzpvf backup.tgz -C /cpsys/tmp/ -T list.txt     |
|                              列出归档包里的内容                               |                        -t, --list                        | 
|                             删除归档里的指定文件                              |                         --delete                         |
|                                                                               |           tar --delete zyc/access -vf zyc.tar            |
|                                打包时排除目录                                 |                        --exclude                         |
|                                                                               |           tar 选项 目标文件 --exclude= 源文件            |
|                                                                               |              --exclude 应该放在目标文件前面              |
|                                                                               |   源文件的格式是 `/proc` 或 `/proc/*`，不能写 `/mnt/`    |
|                                                                               | 对于绝对路径还是相对路径，目标文件与相对路径应该保持一致 |
|                                                                               |   tar -zcvf tomcat.tar.gz --exclude=tomcat/logs tomcat   |
|                          向压缩归档文件末尾追加文件                           |                            -r                            |
|                             更新原压缩包中的文件                              |                            -u                            |
| [tar打包的时候如何去掉目录前缀?](https://segmentfault.com/q/1010000000211312) |                                                          |


# 7z 命令

7z command \[switches\] archive \[filelist\]

| 操作 | 命令                                                           | 解释                                                                                                                                  |
| ---- | -------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| 压缩 |                                                                |                                                                                                                                       |
|      | 7z a archive filelist                                          | Add files to archive                                                                                                                  |
|      | 7z a -p                                                        | 把 filelist 里的文件/目录添加到 achive，并设置密码                                                                                    |
| 解压 |                                                                |                                                                                                                                       |
|      | 7z e                                                           |                                                                                                                                       |
|      | 7z x archive                                                   | 解压 achive                                                                                                                           |
|      | 7z x -odirectory archive                                       | Output. <br />把 achive 解压到directory，<br />如果不存在就创建该目录；<br />相对/绝对路径都可；<br />-o与 directory 间没有空格！！！ |
|      | 7z e                                                           |                                                                                                                                       |
| 列出 |                                                                |                                                                                                                                       |
|      | 7z l                                                           |                                                                                                                                       |
|      |                                                                |                                                                                                                                       |
|      | -snh                                                           | store hard links as links                                                                                                             |
|      | -snl                                                           | store symbolic links as links                                                                                                         |
|      | -ssw                                                           | compress shared files                                                                                                                 |
|      | -u\[-\]\[p#\]\[q#\]\[r#\]\[x#\]\[y#\]\[z#\]\[!newArchiveName\] | Update options                                                                                                                        |

大多数配置文件词尾是 rc。”rc”是很多脚本类文件的后缀，这些脚本通常在程序的启动阶段被调用。
来源是 rc ← runcom ← run command

> “rc” 是取自 “runcom”, 来自麻省理工学院在 1965 年发展的 CTSS系统。相关文献曾记载这一段话：”具有从档案中取出一系列命令来执行的功能；这称为 “run commands” 又称为 “runcom”，而这种档案又称为一个 runcom (a runcom)。

