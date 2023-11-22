---
title: Linux 安装输入法
tags:
  - linux
categories:
  - Linux
---
# debian 安装搜狗输入法

```shell
sudo apt purge fcitx* ibus
sudo apt autoremove
sudo apt install fcitx
sudo apt install ./sogoupinyin_4.0.1.2800_x86_64.deb
sudo apt --fix-broken install
sudo apt install libqt5qml5 libqt5quick5 libqt5quickwidgets5 qml-module-qtquick2 libgsettings-qt1
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
