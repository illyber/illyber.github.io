#disk/分区/remove
dd命令删除分区和分区表：
```bash
dd if=/dev/zero of=/dev/sdb4 bs=1M count=1 progress=status
```
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

