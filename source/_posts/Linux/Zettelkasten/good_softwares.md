---
title: good_softwares
categories:
  - Linux
date: 2024-04-02 05:20
tags:
  - linux-set/必装软件
---

---
# Gnome plugin
snap 的 Firefox 安插件有问题，去官网下Firefox（用apt安装），或者用 chrome。

```shell
AppIndicator and KStatusNotifierItem Support #在顶部任务栏显示应用图标（如输入法图标），是Ubuntu的默认插件
bing wallpaper
caffeine
Clipboard Indicator
Dash to Dock (Ubuntu Dock)
desktop icons NG
gsconnect
Simple System Monitor
screenshot tool
Unite #将最大最小按钮融合到顶部
compiz alike lamp effect
No Titlebar When Maximized
debian linux updates indicator
```
archlinux 需安装 `gnome-browser-connector`
# kde生成视频缩略图(thumbnail)
安装 ffmpegthumbs，并在 dolphin 进行相关设置
# OCR
OCR 工具
[OCR](https://blog.csdn.net/weixin_42301220/article/details/124059358)
pot-desktop

# 安装archlinux

安装时改变字体：`setfont /usr/share/kbd/consolefonts/ter-v28n`

或修改 `/etc/default/console-setup` FONTSIZE = "24x12"

- [archlinux的安装和美化](https://arch.icekylin.online/guide/)

- 安装 Archlinux 报错“error: openssl: signature from "Pierre Schmitz <pierre@archlinux.org>" is marginal trust” 时

执行
```shell
sudo pacman -Sy archlinux-keyring

或

pacman -Syu haveged
systemctl start haveged
systemctl enable haveged
rm -fr /etc/pacman.d/gnupg
pacman-key --init
pacman-key --populate archlinux
pacman-key --populate archlinuxcn
```


- [Arch Linux 完全安装教程 2023.6](https://www.bilibili.com/read/cv20753052?from=search&spm_id_from=333.337.0.0). 这里有安装archlinux gnome中文输入法的方法

# 显卡驱动

[超详细! Ubuntu 18.04安装NVIDIA 显卡驱动](https://www.cnblogs.com/zhaoyingjie/p/15380694.html)

[Debian 11安装Nvidia闭源驱动](https://www.cnblogs.com/FrankOu/p/15369195.html)

# 安装 WPS 后提示缺少字体
![image](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281946429.png)
ref: [用法来源](https://blog.csdn.net/cmlin_mumu/article/details/125169651)
1. 下载缺失字体。字体文件：链接: https://pan.baidu.com/s/1sbAT9NIU0s06G0CK-7LqmQ 提取码: es58
2. 下载完成之后，进入字体文件夹，将字体复制到 /usr/share/fonts 中：
```bash
sudo cp * /usr/share/fonts
```
3. 执行下面的命令，生成字体的索引信息：
```bash
sudo mkfontscale
sudo mkfontdir
sudo fc-cache
```
4. 重启wps即可，字体缺失的提示不再出现.

第二个问题是，WPS中的中文字体显示很奇怪，字的大小不一致，而且模糊，看起来别扭。安装如下字体：
```bash
ttf-wqy-microhei #文泉驿-微米黑
ttf-wqy-zenhei #文泉驿-正黑
xfonts-wqy #文泉驿-点阵宋体
```
直接安装字体。

# VBOX
arch 安装 guest 前，要安装 `linux-headers`

# 硬解
gpu驱动

```shell
vaapi
intel_gpu_top
nvidia-smi
```

vaapi
```shell
vainfo
mpv --hwdec=vaapi S01E01.mkv
mpv --hwdec=auto S01E01.mkv
```

vdpau
```shell
vdpauinfo    #可能需要安装这个命令
mpv --hwdec=vdpau S01E01.mkv
```

# flameshot快捷键无法截图
设置快捷键指令为 `sh -c -- "flameshot gui"`




---
