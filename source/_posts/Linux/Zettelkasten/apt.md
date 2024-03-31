2024 0331 15:45
Tags: #package-manager/apt

---
## 添加其它架构支持

dpkg --add-architecture i386 && apt-get update 

## dpkg-reconfigure

重新设置已安装的软件

```shell
dpkg-reconfigure [options] packages
```

## dpkg-preconfigure

let packages ask questions prior to their installation

```shell
dpkg-preconfigure [options] package.deb
dpkg-preconfigure --apt
```



## 仓库分类

Ubuntu 的仓库分类：

- Main - Canonical 支持的**自由开源软件**。
- Universe - 社区维护的**自由开源软件**。
- Restricted - 设备的**专有驱动**程序。
- Multiverse - 受**版权或法律**问题限制的软件。

Debian 的仓库分类：

- free
- contri
- non-free

## 设置软件源

```shell
sudo apt edit-sources
/etc/apt/sources.list 文件
/etc/apt/sources.list.d 文件夹里的文件

add-apt-repository --help  //用 add-apt-repository 这个命令就可以了
sudo add-apt-repository ppa:mozillateam/ppa  
# 对应deb https://ppa.launchpadcontent.net/mozillateam/ppa/ubuntu jammy main 
# 默认网址https://ppa.lunchpadcontent.net，自动识别版本ubuntu jammy
```

## 搜索

```shell
sudo apt search  在更新缓存中搜索
dpkg --search <files>  搜索该文件是由哪个软件包安装的
apt list --installed <pkg>  搜索已安装软件包
```

## 安装软件

```shell
apt install
sudo apt -f install  安装缺少的依赖
sudo apt --fix-broken install  修复依赖的关系
sudo apt install ./package_name.deb # 推荐用这个安装本地deb包，能自动解决依赖；dpkg不能
-y #都选yes
```

## 更新

```shell
apt update
apt upgrade
apt dist-upgrade
```

## 卸载

```shell
sudo apt remove
sudo apt purge
sudo apt remove <pkg> --purge
sudo apt autoremove --purge
```

## 更新ubuntu系统

| 步骤                      |                                                                                                            |
| ------------------------- | ---------------------------------------------------------------------------------------------------------- |
| 指定更新 LTS 版还是普通版 | 更改 /etc/update-manager/release-upgrades 里 Prompt 的选项<br />lts: 稳定版，normal: 普通版，never: 不更新 |
| 更新缓存                  | sudo apt update                                                                                            | 
| 更新软件                  | sudo apt dist-upgrade                                                                                      |
| 更新系统                  | sudo do-release-upgrade                                                                                    |




---
