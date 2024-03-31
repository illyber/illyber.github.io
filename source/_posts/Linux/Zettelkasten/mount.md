2024 0331 16:12
Tags: #disk/分区/mount 

---
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






---
