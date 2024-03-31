
[Ubuntu Document](https://help.ubuntu.com/community/btrfs)
# 子卷/快照
## 删除子卷
子卷里有子卷无法一次性删除，会显示
```shell
ERROR: Could not destroy subvolume/snapshot: Directory not empty
```
需要先删除里面的子卷。
## 删除timeshift 第一个备份恢复后创建的 restore 备份

问题：恢复 timeshift 第一个备份后自动生成的备份无法被删除，如下图
![t2.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/t2.png)

![t3.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/t3.png)


原因：before restoring的备份里还有子卷machines和portables。必须要先删除内部的子卷。
![t4.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/t4.png)

解决方法：
1. 点击 timeshift->browser. 按上图的路径找子卷
![t5.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/t5.png)

2. 复制地址，在终端里删除machines和portables两个子卷
![t6.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/t6.png)
![t7.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/t7.png)

3. 这样就可以在timeshift里直接删除 'before restoring'这个子卷

# 显示使用空间
```shell
btrfs filesystem usage /
```
# 挂载快照
[Linux btrfs 文件系统快照备份与恢复（恢复为挂载快照为根文件系统或进入 initramfs 环境）](https://www.learndiary.com/2021/11/btrfs-snapshot-restore/)

# 可读写性
help 信息
```shell
btrfs property get [-t <type>] <object> [<name>]
    Get a property value of a btrfs object
btrfs property set [-f] [-t <type>] <object> <name> <value>
    Set a property on a btrfs object
btrfs property list [-t <type>] <object>
    Lists available properties with their descriptions for the given object
```
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202311221559934.png)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202311221602960.png)

# 快照备份
软件：
1. timeshift, snapper
2. grub-btrfs

3. snap-pac, snap-pac-grub
snap-pac: Pacman hooks that use snapper to create pre/post btrfs snapshots like openSUSE's YaST
snap-pac-grub: Pacman hook to update GRUB entries for grub-btrfs after snap-pac made snapshots