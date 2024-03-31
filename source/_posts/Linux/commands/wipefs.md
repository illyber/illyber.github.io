#disk/分区/remove
`wipefs /dev/sda -a`

分区表是硬盘的分区信息，要删除一个硬盘的所有分区表很麻烦的，需要fdisk一个一个的删除，其实dd命令可直接清除分区信息，当然，这也是linux给root用户留下的作死方法之一。