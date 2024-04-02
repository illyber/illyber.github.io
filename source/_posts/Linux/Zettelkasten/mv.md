---
title: mv
categories:
  - Linux
date: 2024-04-02 05:20
tags:
  - 基本命令/mv
---

---

# 移动多个文件

1. 需要注意的是，目录 target_dir 必须在最后面，而且它前面不能再出现其他目录
```bash
mv file1 file2 file3 target_dir
```
2. 还可以用 -t 选项指定目标文件夹
```bash
mv file1 file2 file3 -t target_dir
```
3. 利用通配符
```bash
# 把所有字体移向fonts
mv ~/Downloads/*ttf ~/myprofiles/fonts/
```


---
