---
title: docker 常用命令
tags:
  - docker
categories:
  - Tool
---
# 登录账号
```
//退出容器进入宿主机执行  
docker exec -it --user=work test bash
```

# ssh
参考：[极品小男 - SSH连接docker中的container](https://zhuanlan.zhihu.com/p/113962350)

1. 设置端口映射. `sudo docker run -p 10022:22 --name=debian --hostname=deb -it debian bash`
2. 没有密码的话需要设置密码，ssh 连接时需要. `passwd`
3. 安装 ssh. `apt install ssh vim`
4. 修改 ssh 配置文件 /etc/ssh/sshd_config
```ssh
vim /etc/ssh/sshd_config

PubkeyAuthentication yes #启用公钥私钥配对认证方式
PermitRootLogin yes #root能使用ssh登录
port=22 #开启22端口
```
4. 重启 ssh 服务. `service ssh start`
5. 不知道为什么，ssh 连接 docker container 时用主机名不行，用 ip 地址。`ssh user_name@ip_address`

ip 命令在 iproute2 软件包里。

# 端口映射
在创建容器时指定端口
```shell
sudo docker run -p 10022:22 --name=debian --hostname=deb -it debian bash
```