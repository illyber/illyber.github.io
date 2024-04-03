---
title: disk-commands
date: 2024-04-02 03:30
tags: 
categories:
  - Linux
---

# 查看信息
```shell
df -h     #查看磁盘占用
du -h     #查看目录占用
sudo du -h /var/ | sort -rh | head -5 #打印/var目录的前5大文件与目录
fdisk -l  #显示分区起点终点
lsblk -f  #显示分区ＵＵＩＤ和其它信息，通过blkid实现的
blkid：显示分区ＵＵＩＤ
btrfs subvolume list -p /mnt #列出子卷
```

# 创建分区和子卷
- （创建分区）不应在挂载时分区
```shell
fdisk
cfdisk
parted
gparted
gdisk  #支持gpt任意多个分区
```
- 创建子卷（必须创建btrfs和挂载后）
```shell
btrfs subvol create /mnt/@ # 创建 / 目录子卷
btrfs subvol create /mnt/@home # 创建 /home 目录子卷
```
# 格式化分区/创建文件系统
不应在挂载时建立文件系统。创建文件系统后才能挂载到系统
```shell
#mkfs 格式化

#主分区
sudo mkfs.ext4 /dev/sda2
		-L 选项可为分区添加标签
		
#EFI分区
sudo mkfs.fat -F 32 /dev/sda1

#swap分区
sudo mkswap /dev/sda3
```

