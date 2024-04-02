---
title: boot
categories:
  - Linux
date: 2024-04-02 03:30
tags:
  - boot
---

LegacyBIOS/UEFI BIOS -> grub/MBR/GPT

# 显示开机信息

dmesg (display message)

# initramfs

archlinux 是 initramfs-linux.img, debian 是 initrd.img (名字如此，实质还是initramfs)
启动时，先加载 vmlinuz, 再加载 initramfs

生成initramfs用`update-initramfs`命令

## debian的initramfs

配置文件：/etc/initramfs-tools/initramfs.conf

|                     | 命令             | 解释                                             |
| ------------------- | ---------------- | ------------------------------------------------ |
| 生成 initramfs      | mkinitramfs      | low-level tool for generating an initramfs image |
| 更新 initramfs      | update-initramfs | 调用mkinitramfs实现的                            |
| 解压 initramfs      | unmkinitramfs    | extract content from an initramfs image          |
| 查看 initramfs 内容 | lsinitramfs      | list content of an initramfs image               |


```shell
/etc/initramfs-tools/
├── conf.d
│   ├── driver-policy
│   └── resume
├── hooks
├── initramfs.conf
├── modules
├── scripts
│   ├── init-bottom
│   ├── init-premount
│   ├── init-top
│   ├── local-bottom
│   ├── local-premount
│   ├── local-top
│   ├── nfs-bottom
│   ├── nfs-premount
│   ├── nfs-top
│   └── panic
└── update-initramfs.conf
```

## archlinux的initramfs
生成 `initramfs-linux.img`，用 `mkinitcpio -P`命令，这个命令一般会自动运行。
mkinitcpio的主配置文件是`/etc/mkinitcpio.conf`。此外，内核软件包的预配置文件位于`/etc/mkinitcpio.d`（例如：`/etc/mkinitcpio.d/linux.preset`）。

`initramfs-linux.img`位于 `/boot`目录下。

# grub和启动项

[Linux系统启动管理](http://c.biancheng.net/linux_tutorial/12/)

## 安装grub

```shell
#安装 GRUB 到 EFI 分区：
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=ARCH

--target=x86_64-efi   平台为x86_64-efi
--efi-directory=/boot/efi —— 将 grubx64.efi 安装到之前的指定位置（EFI 分区）
--bootloader-id=ARCH —— 取名为 ARCH
-d, --directory=/boot    use images and modules under DIR [default=/usr/lib/grub/<platform>]
```

## Debian 生成grub.cfg文件

![生成grub.cfg](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202302041453740.svg)

## 添加其它启动grub
编辑 /etc/grub.d/40_custom 文件
```shell
#!/bin/sh                                                                                                   
exec tail -n +3 $0
# This file provides an easy way to add custom menu entries.  Simply type the
# menu entries you want to add after this comment.  Be careful not to change
# the 'exec tail' line above.
menuentry 'Arch' --class archlinux {
   insmod part_gpt
   insmod btrfs
   set root='hd1,gpt8'
   #root是boot分区
   search --no-floppy --fs-uuid --set=root FDD2-3FD3
   chainloader /EFI/archlinux/grubx64.efi
   #efi
}
```


## 美化

|                          | 软件                       | 主题                                                           |
| ------------------------ | -------------------------- | -------------------------------------------------------------- |
| 开机 logo                | hackbgrt.exe（见百度网盘） |                                                                |
|                          |                            |                                                                |
| 启动项选择页面和过场背景 | grub-customizer            |                                                                |
|                          | grub theme                 | [Fate Series GRUB Theme](https://www.gnome-look.org/p/1850334) |
|                          |                            |                                                                |
| 开机加载动画             | plymouth, plymouth-theme   |                                                                |
|                          | plymouth theme             | [nibar](https://www.gnome-look.org/p/1784844)                  |
| 背景图片                 | /etc/default/grub          | GRUB_GFXMODE="1920x1080"                                       |

## 删除启动文件

easyuefi 百度网盘有破解版。

## U盘启动盘恢复为普通U盘

1. cmd里输入 diskpart
2. 新窗口里 list disk->选择U盘 select disk 几->clean
![](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281946414.png)
![](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281946415.png)

## bios 选项里没有 Windows10 选项

`os-prober`探测程序.

[关于grub的结构](https://blog.csdn.net/u012433948/article/details/51138542)

运行`sudo update-grub`。（只有在非管理员账号用 sudo 才能运行 update-grub）
出现警告
`Warning: os-prober will not be executed to detect other bootable partitions`

解决方法：在/etc/default/grub文件中添加，
`GRUB_DISABLE_OS_PROBER=false`
再更新 grub.cfg
`sudo update-grub`

# 挂载EFI分区
典型挂载点. 来自[EFI 系统分区](https://wiki.archlinuxcn.org/wiki/EFI_%E7%B3%BB%E7%BB%9F%E5%88%86%E5%8C%BA#%E5%85%B8%E5%9E%8B%E6%8C%82%E8%BD%BD%E7%82%B9)
有三种挂载EFI系统分区的典型情况：

- 挂载 EFI系统分区 到 /boot：
便于系统维护和管理，/boot是微码包安装CPU微码、initramfs文件和mkinitcpio安装内核与initramfs镜像的默认位置。
FAT在挂载时设置了全局属性，这会阻止设置文件特定的权限和拓展属性
通常安装在/boot中的文件与EFI相关文件共享EFI系统分区，提高了EFI系统分区的大小需求
双启动的情况下，系统特定的启动文件会处在被其它系统修改操作的潜在危险中
无法加密/boot，因为固件需要读取EFI相关文件
- 挂载 EFI系统分区到/efi：
当EFI系统分区包含其他系统的文件时最好和操作系统相关的文件分开，这确保了操作系统相关和EFI相关文件的分离。
只有EFI二进制文件（引导加载程序（和可选驱动））和（或）统一内核镜像会安装在EFI系统分区，避免了安装在/boot中的文件对EFI系统分区的大小需求，节约了EFI系统分区的空间。
允许保留/boot中文件的Linux特定的文件系统权限，避免了FAT的限制。
允许根据需求单独挂载EFI系统分区，例如需要升级引导加载程序时。
如果加密整个系统并且配置恰当，除少数需要文件没有被加密，/boot中的文件能够被加密保护：内核及其他文件储存在加密分区，统一内核镜像或引导加载程序通过相应的文件系统驱动来访问这些文件。
- 挂载 EFI系统分区到/efi， 然后再挂载一个“拓展引导加载器分区”（XBOOTLDR）分区到 /boot。
在以前创建的 ESP 太小而无法容纳多个引导加载程序以及内核但 ESP 又无法轻松调整大小时（例如
在 Windows 之后将 Linux 安装到 双引导（多引导） 时），这可能非常有用。至少在 systemd-
boot#使用XBOOTLDR安装 时支持此方法。
- 注意：
/efi是/boot/efi的替代挂载点，/boot/efi在过去被使用但现在不推荐。
/efi在安装一开始时不存在，需要先用 mkdir 创建再挂载EFI系统分区到该目录。

# 启动过程
启动时，先加载 vmlinuz, 再加载 initramfs
笼统的来说，不生成initramfs的情况下，启动顺序为：
1. grub引导vmlinuz，vmlinuz有root参数，例如root=/dev/sda7，或者root=UUID
2. vmlinuz读取/etc中的modules文件，决定载入哪个模块（这里一般放置网络模块等，例如vbox虚拟机驱动vboxdrv，我的网卡brcmsmac，b43等），模块大概是放在/lib/modules*。此时要求vmlinuz编译了可以读取 / 的文件系统。

# 添加40_custom
```grub
#!/bin/sh                                                                                             
exec tail -n +3 $0
# This file provides an easy way to add custom menu entries.  Simply type the
# menu entries you want to add after this comment.  Be careful not to change
# the 'exec tail' line above.
menuentry 'Arch' --class archlinux {
   insmod part_gpt
   insmod btrfs
   set root='hd1,gpt1'
   #root是boot分区
   search --no-floppy --fs-uuid --set=root 233B-9417
   chainloader /EFI/ARCH/grubx64.efi
   #efi
}
```

# 编辑UEFI启动项
efibootmgr
```shell
efibootmgr              显示所有UEFI启动项
efibootmgr -v           显示所有UEFI启动项及详细信息
efibootmgr -b 0001 -B   删除编号为0001的启动项
```

# grub后的动画--plymouth

1. 要安装plymouth-themes, 在/etc/default/grub的GRUB_CMDLINE_LINUX_DEFAULT变量添加splash

2. debian系统的主题位于 /usr/share/plymouth/themes/

3. ```bash
   plymouth-set-default-theme	显示当前使用的plymouth主题
   plymouth-set-default-theme -l	显示所有的主题
   plymouth-set-default-theme -R <theme-name>	设置theme-name为主题
   	-R, --rebuild-initrd   Rebuild initrd (necessary after changing theme)
   ```

4. You may need to add some boot parameters, to make the boot animation more "fluently". Some examples: "quiet splash loglevel=3 rd.udev.log_level=3"