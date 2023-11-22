---
title: Linux 主机和账户设置
tags:
  - linux
categories:
  - Linux
date: updated
---
参见《Linux命令行与shell脚本编程大全》
# 主机
修改主机名：`sudo hostnamectl set-hostname <new_hostname>`
                    `hostname new_hostname`
查看主机名：`hostname` 或 `hostnamectl`

# 添加账户 (useradd)
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
# 删除账户
userdel 选项 用户名

```shell
-r 把用户的主目录一起删除
```
# 修改账户 (usermod)
usermod 选项 用户名

常用的选项包括-c, -d, -m, -g, -G, -s, -u以及-o等，这些选项的意义与useradd命令中的选项一样，可以为用户指定新的资源值。
```shell
#debian, 添加用户到souders
su
sudo usermod -aG sudo <username>
```

# 切换账户
切换到其它账户： `su other_account`

# 修改密码
修改 account 的密码： `passwd account`

# 列出所有账户
- `cat /etc/passwd`