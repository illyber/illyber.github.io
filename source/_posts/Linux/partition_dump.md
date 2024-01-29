---
title: Linux 硬盘和分区
tags:
  - linux
categories:
  - Linux
date: updated
---
# 硬盘和分区

## fstab
```shell
genfstab -U /mnt > /mnt/etc/fstab

#修改fstab后生效
systemctl daemon-reload
```

## 查看信息
```shell
df -h     #查看磁盘占用
du -h     #查看目录占用
sudo du -h /var/ | sort -rh | head -5 #打印/var目录的前5大文件与目录
fdisk -l  #显示分区起点终点
lsblk -f  #显示分区ＵＵＩＤ和其它信息，通过blkid实现的
blkid：显示分区ＵＵＩＤ
btrfs subvolume list -p /mnt #列出子卷
```

## 设置文件系统标签
1. for ext2/ext3/ext4
```shell
e2label device [newlabel]
```
2. for dos(vfat, fat16, fat32, etc.)
```shell
dosfslabel device [label]
```
3. for swap
```shell
swaplabel -L [label] dev
```
4. for ntfs
```shell
ntfslabel [options] device [label]
```
5. for xfs
```shell
xfs_admin -L [label] dev
```
6. for btrfs
```shell
sudo btrfs filesystem label /dev/sdxN my_label
```
## 创建分区和子卷
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
## 格式化分区/创建文件系统
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
## 挂载卸载分区
格式化之后才挂载。按一定顺序挂载分区和子卷
```shell
mount -t btrfs -o subvol=/@,compress=zstd /dev/sdxn /mnt # 挂载到 / 目录
mkdir /mnt/home # 在刚挂载的分区上创建 /home 目录

mount -t btrfs -o subvol=/@home,compress=zstd /dev/sdxn /mnt/home # 挂载到 /home 目录
mkdir -p /mnt/boot/efi # 创建 /boot/efi 目录

mount /dev/sdxn /mnt/boot/efi # 挂载 /boot/efi 目录

swapon /dev/sdxn # 挂载交换分区
swapoff /dev/sdxn # 卸载交换分区
```

## 删除分区

```shell
parted
wipefs /dev/sda -a
dd if=/dev/zero of=/dev/sdb4 bs=1M count=1 progress=status
```

dd命令清除分区和分区表

分区表是硬盘的分区信息，要删除一个硬盘的所有分区表很麻烦的，需要fdisk一个一个的删除，其实dd命令可直接清除分区信息，当然，这也是linux给root用户留下的作死方法之一。

dd 命令主要参数如下：
- if=　in file 输入文件，linux下文件的概念应用范围相当广，通常是普通光盘镜像文件或者块设备
- of=　out file 输出文件，通常是普通光盘镜像文件或者块设备
- bs=　buffer size 缓存区大小，你可以认为dd命令读取一块输入文件到buffer(缓存区)，然后将缓存区的内容吸入到输出文件。通常可将bs=1M或者bs=1KB之类的。
- count= 读取输入文件的最多次数。默认情况下，dd命令直接把输入文件已知读取到文件末尾，这个参数可以控制读取的大小。
- skip= 跳过文件开头的大小。默认错排能个文件开头开始读取。
- 例子：将U盘当前状态保存下来成为一个文件,
```
dd if=/dev/sdb of=/backup/ISO/Upan/save.iso
```

清空硬盘的分区信息（慎重使用）
```
dd if=/dev/zero of=/dev/sdb bs=1M count=1 status=progress
```

# 迁移Linux系统或分区

[使用tar或dd等完成Linux系统备份恢复](https://www.vinchin.com/blog/vinchin-technique-share-details.html?id=412)

## 用cp迁移分区
- 保留权限复制
```shell
cp /mnt/usr/* /mnt/new -prv  ##preserve, recursive, verbose
```

- 复制分区后可能要进行的操作，否则挂载后运行会提示无权限
```shell
sudo chown root:root /usrtmp/bin/sudo
sudo chmod 4755 /usrtmp/bin/sudo
```
## rsync
remote sync
适用于大文件和跨文件系统传输，和远程传输。
```shell
rsync -P source destination
```
`-P` 与 `--partial --progress` 选项的作用是相同的，该选项使得文件可以分块传输并显示传输过程中的进度。
`-r`/`--recursive` 递归到目录中传输。

## 用tar迁移
- 压缩原系统
```shell
tar -pcvf /media/hdg/usb/tar-img.tar --exclude=/mnt/* --exclude=/lost+found --exclude=/proc/* --exclude=/sys/* --exclude=/tmp/* --exclude=/dev/* --exclude=/media/*  --exclude=/run/* /
```

- 用live CD，解压到新硬盘
```shell
tar -xvf /media/hdg/usb/tar-img.tar -C /mnt
```

- 挂载 /proc, /sys, /dev
```shell
mount -t proc /proc proc/
mount --rbind /sys sys/
mount --rbind /dev dev/

或者
mount /dev/sdaN /mnt
mount --rbind /dev  /mnt/dev
mount --rbind /proc /mnt/proc
mount --rbind /sys  /mnt/sys
chroot /mnt bash
grub-install /dev/sda
```

- chroot 切换到/mnt

- 安装grub到硬盘

如果恢复到的硬盘的引导分区MBR和原备份文件时的不一致，可能会导致无法开机，可重设grub引导来避免此情况。

因为grub安装在分区表那一部分

```shell
grub-install /dev/sda
grub-install --recheck /dev/sda
```

- 或许更新grub

```shell
sudo update-grub
```

## 用dd迁移(dd比tar快多了！)

/dev/sda到/dev/sdb

```shell
dd if=/dev/sda bs=1M | zstd -T0 > dd.img.zst
zstd dd.img.zst -T0 -dc | dd of=/dev/sdb bs=1M
```
## 用dump迁移
## btrfs迁移

必须是只读快照才能 send/receive

```shell
btrfs send <snapshot> | btrfs receive <snapshot>
```



# chroot注意事项

- 解决chroot后域名解析失败的问题
在执行chroot命令前，拷贝Live的DNS解析。即: `sudo cp /etc/resolv.conf /mnt/etc/resolv.conf`
- 磁盘信息/设备信息
```shell
mount -t proc /proc /mnt/proc/
mount --rbind /sys /mnt/sys/
mount --rbind /dev /mnt/dev/
```
[mount bind功能详解](https://www.junmajinlong.com/linux/mount_bind/index.html?)
-t: type
--bind:  
    mount --bind olddir newdir
    这里，olddir 是一个已经挂载的挂载点中的某个子目录。mount bind绑定后的两个目录类似于
硬链接，无论读写olddir还是读写newdir，都会反应在另一方，内核在底层所操作的都是同一个物理位置。如果卸载了原挂载点olddir，newdir仍旧可以访问原olddir的内容。此时要umount的话，那么就umount newdir.使用 bind 与对同一设备进行两次挂载的区别在于:您可以挂载子目录而无需挂载整
个文件系统。
--rbind:
    --rbind类似于bind，但会递归bind当前挂载点上已有的子挂载点

/proc:
    Linux系统上的/proc目录是一种文件系统，即proc文件系统。与其它常见的文件系统不同的是，/proc是一种伪文件系统（也即虚拟文件系统），存储的是当前内核运行状态的一系列特殊文件，用户可以通过这些文件查看有关系统硬件及当前正在运行进程的信息，甚至可以通过更改其中某些文件来改变内核的运行状态。 
/sys:
    sysfs把连接在系统上的设备和总线组织成为一个分级的文件，它们可以由用户空间存取，向用户空间导出内核的数据结构以及它们的属性。sysfs的一个目的就是展示设备驱动模型中各组件的层次关系.sysfs 文件系统集成了下面3种文件系统的信息：针对进程信息的 proc 文件系统、针对设备的 devfs 文件系统以及针对伪终端的 devpts 文件系统。
/dev:    [Linux /dev目录文件详解](https://zyazhb.github.io/2020/08/30/linux-dev/)
    dev是设备(device)的英文缩写。这个目录中包含了所有Linux系统中使用的外部设备。  
但是这里并不是放的外部设备的驱动程序，它实际上是一个访问这些外部设备的端口。我们可以非常方便地去访问这些外部设备，和访问一个文件，一个目录没有任何区别。  
Linux沿袭Unix的风格，将所有设备认成是一个文件。
# btrfs备份
snapper和btrfs-assistant

# Windows diskpart 删除分区
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202311261825395.png)
