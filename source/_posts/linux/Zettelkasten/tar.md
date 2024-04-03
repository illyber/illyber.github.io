---
title: tar
date: 2024-04-02 05:20
tags:
  - 归档和压缩/tar
categories:
  - Linux
---

---
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






---
