---
title: input_method
date: 2024-04-02 05:20
tags: [linux-set/输入法, 270]
categories:
  - Linux
---

---
[TOC]
# debian安装fcitx5
1. 卸载 ibus
2. 安装fcitx5和中文插件
```bash
sudo apt install fcitx5 fcitx5-chinese-addons
```
3. fcitx5-diagnose命令能诊断输入问题
4. 可能是zsh在登陆时不读取/etc/profile而读取/etc/zprofile造成的，在/etc/zprofile里调用/etc/profile即可：`echo "source /etc/profile" > /etc/zprofile`
	为了保险，再新建一个/etc/environment, 内容为：
```bash
export XIM_PROGRAM=fcitx                                          
export XIM=fcitx
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=“ @im=fcitx” 
```

# archlinux安装ibus-libpinyin

```shell
sudo pacman -S ibus ibus-libpinyin fcitx5
```
如果不行，尝试以下的内容。
本节内容引用自：[Arch Linux 完全安装教程 2023.6 - 哔哩哔哩](https://www.bilibili.com/read/cv20753052?from=search&spm_id_from=333.337.0.0)

中文字体：
```shell
wqy-microhei
wqy-microhei-lite
wqy-bitmapfont
wqy-zenhei
ttf-arphic-ukai
ttf-arphic-uming
adobe-source-han-sans-cn-fonts
adobe-source-han-serif-cn-fonts
noto-fonts-cjk
```

手动安装 ibus 输入法：
```shell
sudo pacman -S ibus ibus-libpinyin
#ibus-libpinyin 是中文输入法引擎，其强于 ibus-pinyin。
```

```shell
ibus-setup
```
只需要执行一次，后续需要 ibus 开自启动在 gnome-tweaks （优化）中添加启动项。

接下来要修改 .bashrc 文件：
```shell
vim ~/.bashrc
添加如下内容：

export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus

上面的内容在运行 ibus-setup 后输出，修改完毕之后重新登陆或重启系统。如果桌面环境使用 gnome，还需要在设置 → 输入源中进行相关设置，详见下文图片
```

使用 tmoe 安装 ibus：
```shell
安装 tmoe：

pacman -S wget
wget l.tmoe.me/2.awk
启动 tmoe：
gawk -f 2.awk
```

选择中文：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202306211422424.png)

选择 tools：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202306211422739.png)

自动安装依赖：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202306211422108.png)

打开 “秘密花园”：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202306211423087.png)

打开 “input method：输入法”：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202306211423261.png)

三个都可以选择，如果安装了 gnome，建议选择 ibus：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202306211423897.png)

选择 “sunpinyin”：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202306211424013.png)

安装完毕：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202306211424047.png)

按下 ctrl + c 退出，重启系统。

在系统设置添加输入法：
不用 Gnome 请跳该部分。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202306211425310.png)

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202306211425902.png)

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202306211425570.png)

使用 win + 空格 切换输入法。

设置ibus开机自启动：
来自：https://kassadin.moe/2019/11/25/028-ibus-initial-setup/
新建 `~/.xprofile` 文件
在里面添加：
```shell
# iBus always on 
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus
ibus-daemon -drx
```

微信，QQ 等国产软件的安装和更多中国化设置见：
```shell
https://wiki.archlinuxcn.org/wiki/建议阅读#中国大陆用户的推荐解决方案
```

# fcitx 自定义短语

> 建议使用 QuickPhrase 快速输入，触发方式是长按逗号之后右划，或者拼音输入法中按 v 触发。在设置界面 插件-快速输入-编辑器 中可以自定义映射。
> 
> 输入任意字符输出任意短语的这种“自定义短语“，目前不考虑 fcitx/fcitx 5 。
> 
> 但如果输入的是合法全拼，可以使用自定义词库的方式实现。

[reference](https://github.com/fcitx5-android/fcitx5-android/issues/174)
# fcitx 5 设置直角引号

Fcitx5 默认的标点符号键位为：
```bash
cat /usr/share/fcitx5/punctuation/punc.mb.zh_CN
```

```
. 。
, ，
? ？
" “ ”
: ：
; ；
' ‘ ’
< 《
> 》
\ 、
! ！
$ ￥
^ ……
_ ——
( （
) ）
[ ·
] 「 」
~ ～
```

1. 在. local 下新建标点键位文件
```bash
mkdir ~/.local/share/fcitx5/punctuation/
touch ~/.local/share/fcitx5/punctuation/punc.mb.zh_CN
```

2. 修改键位文件
```bash
vim ~/.local/share/fcitx5/punctuation/punc.mb.zh_CN

. 。
, ，
? ？
" 『 』
: ：
; ；
' 「 」
< 《
> 》
\ 、
! ！
$ ￥
^ ……
_ ——
( （
) ）
[ ·
] 「 」
~ ～

```

[reference](https://cyrusyip.org/zh-cn/post/2020/11/06/configure-fcitx5-on-ubuntu/)


---
