---
title: local本地化
date: 2024-04-02 03:30
tags:
  - 本地化/主机名
categories:
  - Linux
---

参见《Linux命令行与shell脚本编程大全》
# 主机名
修改主机名：`sudo hostnamectl set-hostname <new_hostname>`
                    `hostname new_hostname`
查看主机名：`hostname` 或 `hostnamectl`

# 账户管理
## 添加账户 (useradd)
useradd 选项 用户名

```shell
#archlinux
useradd -m -G wheel -s /bin/bash <username>
    	-m 创建用户的同时创建用户家目录
    	-G 选项后指定附加组
    	wheel —— wheel 附加组可 sudo 进行提权
    	-s 选项后指定 shell 程序
    	username —— 用户名（请自定义，但不要包含空格和特殊字符）
#arch编辑/etc/sudoers文件
    EDITOR=vim visudo # 这里需要显式的指定编辑器，因为上面的环境变量还未生效
    在/etc/sudoers里注释掉下面这一行
    #%wheel ALL=(ALL:ALL) ALL
    也可用编辑器直接编辑sudoers文件，但用visudo更安全

#设置root账户密码（安装时没有设置root密码）
sudo passwd root
```
选项：
```shell
-d 目录 指定用户主目录，如果此目录不存在，则同时使用-m选项，可以创建主目录。
-m 用户主目录不存在时创建主目录
-g 指定用户所属的用户组。
-G 指定用户所属的附加组。sudo 就是附加组。多个附加组用逗号隔开
-s Shell文件 指定用户的登录Shell。
```

例子1，此命令创建了一个用户sam，其中-d和-m选项用来为登录名sam产生一个主目录 /home/sam
```shell
useradd –d  /home/sam -m sam
```

例子2，此命令新建了一个用户gem，该用户的登录Shell是 `/bin/sh`，它属于group用户组，同时又属于adm和root用户组，其中group用户组是其主组。
```shell
useradd -s /bin/sh -g group –G adm,root gem
```
## 删除账户
userdel 选项 用户名

```shell
-r 把用户的主目录一起删除
```
## 修改账户 (usermod)
usermod 选项 用户名

常用的选项包括-c, -d, -m, -g, -G, -s, -u以及-o等，这些选项的意义与useradd命令中的选项一样，可以为用户指定新的资源值。
```shell
#debian, 添加用户到souders
su
sudo usermod -aG sudo <username>
```

## 切换账户
切换到其它账户： `su other_account`

## 修改密码
修改 account 的密码： `passwd account`

## 列出所有账户
- `cat /etc/passwd`

# 时间
- [GMT](https://sspai.com/link?target=https%3A%2F%2Fbaike.baidu.com%2Fitem%2F%25E4%25B8%2596%25E7%2595%258C%25E6%2597%25B6%2F692237)：Greenwich Mean Time，即格林尼治标准时间，也就是世界时。GMT 以地球自转为基础的时间计量系统，但由于地球自转不均匀，导致 GMT 不精确，现在已经不再作为世界标准时间使用。
- [UTC](https://sspai.com/link?target=https%3A%2F%2Fbaike.baidu.com%2Fitem%2F%25E5%258D%258F%25E8%25B0%2583%25E4%25B8%2596%25E7%2595%258C%25E6%2597%25B6%2F787659)：Universal Time Coordinated，即协调世界时。UTC 是以原子时秒长为基础，在时刻上尽量接近于 GMT 的一种时间计量系统。为确保 UTC 与 GMT 相差不会超过 0.9 秒，在有需要的情况下会在 UTC 内加上正或负闰秒。UTC 现在作为世界标准时间使用。
- RTC：Real-Time Clock，即实时时钟，也就是BIOS存储的硬件时间。

世界上不同地区所在的时区是不同的，这些时区决定了当地的本地时间。比如北京处于东八区 (CST)，即北京时间为 UTC + 8，如果 UTC 时间现在是上午 6 点整，那么北京时间为 14 点整。

Windows 与 Linux 看待硬件时间的方式不同。Windows 把电脑的硬件时钟（RTC）看成是本地时间，即 RTC = Local Time，Windows 会直接显示硬件时间；而 Linux 则是把电脑的硬件时钟看成 UTC 时间，即 RTC = UTC，那么 Linux 显示的时间就是硬件时间加上时区。

查看硬件时间和时区 `timedatectl status` or `hwclock`