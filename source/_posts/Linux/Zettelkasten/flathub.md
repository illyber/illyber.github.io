---
title: flathub
categories:
  - Linux
date: 2024-04-02 05:20
tags:
  - 包管理器/flathub
---

---

# flathub
## 添加国内源
```shell
sudo flatpak remote-modify flathub --url=https://mirror.sjtu.edu.cn/flathub
#如果出现错误可尝试：
wget https://mirror.sjtu.edu.cn/flathub/flathub.gpg
sudo flatpak remote-modify --gpg-import=flathub.gpg flathub
```
## 移除远程仓库
```shell
flatpak remote-delete flathub
```
## 添加远程仓库
最方便的方式添加远程仓库是使用 `.flatpakrepo` 文件，它包含远程仓库的信息和GPG秘钥：
```shell
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```



---
