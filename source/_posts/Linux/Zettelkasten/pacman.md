2024 0331 15:49
Tags: #package-manager/pacman

---
# pacman

[pacman linux命令在线中文手册](http://linux.51yip.com/search/pacman)
[pacman常用命令](https://hustlei.github.io/2018/11/msys2-pacman.html)

```shell
pacman <operation> [options] [targets]
#operation 是大写，options 是小写
```
## 密钥错误
如果报密钥相关错误，执行
```shell
pacman -Syu haveged
systemctl start haveged
systemctl enable haveged

rm -fr /etc/pacman.d/gnupg
pacman-key --init
pacman-key --populate archlinux
pacman-key --populate archlinuxcn
新闻
```

## 更新系统

```shell
pacman -Sy #从服务器下载新的软件包数据库。不推荐，推荐-syu.
pacman -Su #升级所有已安装的软件包。
# pacman 可以用一个命令就可以升级整个系统。花费的时间取决于系统有多老。这个命令会同步非本地(local)软件仓库并升级系统的软件包
pacman -Syyu #两个y表示强制刷新软件包数据库
# pacman只能更新全部软件，不能只更新部分软件
```

## 搜索程序


```shell
#远端sync
-S, --sync：在远端软件仓库搜索
-Q, --query：在本地搜索

-s, --search：搜索单个程序名和描述. apply to -Q, -S
-g, --gropus：搜索软件包组
-i, --info：  Display information on a given package. The -p option can be used if querying a package file instead of the local database. Passing two --info or -i flags will also display the list of backup files and their modification states.
-l, --list：列出内容
-u, --sysupgrade：apply to -S
-u, --upgrades：apply to -Q
-t, --required：Restrict or filter output to print only packages neither required nor optionally required by any currently installed package. Specify this option twice to include packages which are optionally, but not directly, required by another package.
-q, --quiet：减少输出内容
-v, --verbose

#远端search
pacman -Ss 关键字   #在仓库中搜索含关键字的软件包（本地已安装的会标记）
pacman -Sl <repo>  #显示软件仓库中所有软件的列表
				   #可以省略，通常这样用 pacman -Sl | 关键字
pacman -Sg         #列出软件仓库上所有的软件包组
pacman -Sg 软件包组 #搜索该软件包

# 本地query（搜索）
# 省略参数默认以选项显示安装的所有程序
pacman -Q  软件名 #在软件包名搜索，显示软件包名称和版本
pacman -Qs 关键字 #在软件包名和软件描述里搜，显示软件包名称和版本
pacman -Qg 软件包 #搜索软件包组
pacman -Qq 软件名 #搜索后显示简洁的结果
pacman -Qi 软件名 #查看某个软件包信息，显示较为详细的信息，包括描述、构架、依赖、大小等等
pacman -Ql 软件名 #列出软件包内所有文件，包括软件安装的每个文件、文件夹的名称和路径

pacman -Qu       #列出所有可升级的软件包
pacman -Qt       #列出不被任何软件要求的软件包
```

## Pactree
注意： pactree(8)不再是pacman包的一部分。它现在在pacman-contrib包中。
要显示软件包的依赖树：

```shell
pactree package_name
#检查一个安装的软件包被那些包依赖，将递归标识-r传递给 pactree，或者使用 pkgtoolsAUR中的whoneeds
```

## 清理缓存

```shell
清理缓存
pacman -Sc：清理未安装的包文件，包文件位于 /var/cache/pacman/pkg/ 目录。
pacman -Scc：清理所有的缓存文件。
```

## 安装

```shell
pacman -S 软件名 #安装软件。也可以同时安装多个包，只需以空格分隔包名即可。
pacman -S --needed 软件名1 软件名2 #安装软件，但不重新安装已经是最新的软件。
pacman -Sy 软件名：安装软件前，先从远程仓库下载软件包数据库(数据库即所有软件列表)。
pacman -Sv 软件名：在显示一些操作信息后执行安装。verbose
pacman -Sw 软件名 #只下载软件包，不安装。

pacman -U 软件名.pkg.tar.gz：安装本地软件包。
pacman -U http://www.example.com/repo/example.pkg.tar.xz  #安装一个远程包（不在 pacman 配置的源里面）。
```

## 卸载

```shell
pacman -R 软件名 	#该命令将只删除包，保留其全部已经安装的依赖关系
pacman -Rs 软件名 	#删除软件，同时删除本机上只有该软件依赖的软件。
pacman -Rc 软件名    #删除软件，并删除所有依赖这个软件的程序，慎用
pacman -Ru 软件名 	#删除软件,同时删除不再被任何软件所需要的依赖
pacman -Rsunv
pacman -Rv 软件名 	#删除软件，并显示详细的信息

-s, --recursive
-n, --nosave
-u, --unneeded
-c, --cascade
-v, --verbose
```

# yay

```shell
#若yay安装失败, 执行下面命令
sudo pacman -Sy archlinuxcn-keyring
yay -R 		# 卸载软件
yay -Rns 	# 卸载该软件及所有不必要软件

yay -Ps		# 显示已安装软件包和系统健康状况的统计数据

pacman -Qm	# If you're looking for packages not installed from the main repos(ie AUR or pkgbuild), use 
```





---
