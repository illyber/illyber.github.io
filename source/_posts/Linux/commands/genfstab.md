# genfstab
#disk/分区/fstab 
生成fstab文件
```shell
genfstab -U /mnt > /mnt/etc/fstab

#修改fstab后生效
systemctl daemon-reload
```

