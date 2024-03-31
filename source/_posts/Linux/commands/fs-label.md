# fs label
#disk/分区/label
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
