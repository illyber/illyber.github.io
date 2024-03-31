---
title: Git notes
tags:
  - git
categories:
  - Tool
---

# 基本概念
工作区（workspace）、暂存区（staging area）、本地仓库（local repository）、远程仓库（remote repository）
暂存（add/stage）、提交（commit）

![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202306222034730.png)


# 克隆到目录

```shell
git clone <repo> <directory>	从 repo 克隆到指定目录
```

# 创建仓库

```shell
git init				将当前目录初始化为仓库
git init <directory>	将指定目录初始化为仓库
```

# 工作区

```bash
使用 "git restore <文件>..." 丢弃工作区的改动
```



# 添加/取消 暂存区

取消暂存

```shell
使用 "git restore --staged <文件>..." 以取消暂存，将更改移动到工作区。
```

当我们需要删除暂存区或分支上的文件, 同时工作区也不需要这个文件了, 可以使用
```shell
git rm file_path  
git commit -m 'delete somefile'  
git push
```

当我们需要删除暂存区或分支上的文件, 但工作区又需要使用, **只是不希望这个文件被版本控制**, 可以使用
```shell
git rm --cached file_path  
git commit -m 'delete remote somefile'  
git push
```

# 查看暂存区

```shell
git status --short(s)	查看工作区和暂存区的状态
git ls-files			查看暂存区内容
	--cached(-c)		显示暂存区中的文件，git ls-files命令默认的参数
	--modified(-m)		显示修改过的文件
	--deleted(-d)		显示删除的文件
	--other(-o)			显示没有被 add 的文件
	--stage(-s)			显示mode以及文件对应的Blob对象，进而我们可以获取暂存区中对应文件里面的内容。
```

# commit

## 提交操作

```shell
git commit <file>
git commit <file> -m <msg>		提交 file 并添加信息
git commit -m <msg>			    commit暂存区所有文件
git commit -a				    commit暂存区和工作区的所有文件           
```

## 查看提交记录

```shell
git log
--patch(p)		显示每次提交的差异
-p -2		显示最近两次提交的差异
--online	简洁版本
git show <hash>	显示 hash 对应的更改
```

## commit 技巧
[Git tips – 同一个文件修改了多处如何分作多个提交](https://ttys3.dev/post/git-how-to-commit-only-parts-of-a-file/)
[原子提交技巧](https://www.zhihu.com/question/19946553/answer/29068386?utm_id=0)

# branch

## 分支操作

```shell
git branch [--list]								    列出branch
git branch <name>                                   新建名为name的分支
初始化了仓库之后要提交到缓存，才能创建新分支。
# git checkout -b <name>                              新建并切换到name分支
git switch <branch>									切换到分支. checkout命令有歧义，不建议用.
git branch -d <branch>							    删除 branch

git checkout <branch>							    切换到 branch

git merge <branch>								    合并 branch
git merge <branch> --allow-unrelated-histories		允许合并无关的历史
git mergetool                                       启动一个合适的可视化合并工具
```

# 远程操作

gitee.com:xavierme/c-primer-plus
[关联多个远程仓库](https://zhuanlan.zhihu.com/p/624682400)

## 拷贝一个仓库到本地

```shell
git clone <url>
git clone https://github.com/tianqixin/runoob-git-test

#重命名为 another-ruboob-name
git clone https://github.com/tianqixin/runoob-git-test another-runoob-name
```

## 连接到远端仓库

```shell
ssh-keygen -t rsa -C <youremailaddress>在 ~/.ssh/ 里生成公钥
	在 GitHub/Gitee 设置里添加公钥
	
git remote add <shortname> git@gitee.com:<用户名>/<仓库名>添加远端仓库源到本地仓库。ssh格式。
git remote rm <shortname>删除连接
git remote rename old_name new_name  # 修改仓库名
git remote查看当前配置有哪些远程仓库
git remote -v执行时加上 -v 参数，可以看到每个别名的实际链接地址。
```

## 从远端拉取代码到本地

```shell
git pull <远程主机名> <远程分支名>:<本地分支名>
git pull简写
git pull origin master如果远程分支是与当前分支合并<br />则冒号后面的部分可以省略
git pull origin master:brantest将远程主机 origin 的 master 分支拉取过来<br />与本地的 brantest 分支合并

merge/rebase
git fetch origin    获取远程更新
git merge origin/master   把更新的内容合并到本地分支
git pull=git fetch + git merge
```

## 把本地代码推到远端

```shell
git push <远程主机名> <本地分支名>:<远程分支名>
git push简写
git push <远程主机名> <本地分支名>如果本地分支名与远程分支名相同<br />则可以省略冒号：
git push origin master将本地的 master 分支推到远端的分支
git push -u origin master
ssh -T git@gitee.com  设置免密推送（直接用ssh格式而不是https格式就不用这个操作）
```

# git设置

```shell
git config [--global] core.editor "vim"		设置vim为默认编辑器
git config [--global] user.email "email"	设置邮箱，省略 --global 只在当前仓库设置
git config [--global] user.name "yourname"	设置用户名
git config [--global] color.ui true			设置颜色
git config --list						查看全局配置
git config --global --unset user.name		移除全局用户名
git config --global user.name				查看全局用户名
git config --global --unset user.email		移除全局邮箱
git config --global user.email				查看全局邮箱
git config --global --unset user.password	移除全局密码
git config --global user.password			查看全局密码
```


# 查看修改

## git diff

用来找出仓库或者文件之间的差异，可以用来预测或者阻止可能产生冲突的合并
```shell
# 工作区 vs 暂存区
git diff
# 工作区 vs 版本库
git diff head
# 暂存区 vs 版本库
git diff –cached
```
有多种方法查看两次提交之间的变动，如下面是一些示例。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202306190314386.png)

## git log

```shell
# 查看最近一次commit的改变
git log -p file

# 查看所有commit记录
git log
git log file
```

# .gitignore 设置
位于工作区目录内
```shell
vim/.vim/view/
# 忽略./vim/.vim/view/目录下的所有文件
```

这里面有一些特殊情况需要考虑，比如某文件已经被提交过了，之后再对他做了一个`.gitignore`的忽略的话。忽略是不会生效的，需要我们手动先将缓存删除。
```shell
# 删除本地的缓存
git rm -r --cached filepath
```

为了添加（开始跟踪）一个特意不跟踪（即忽略）的文件，用户需要使用命令
```shell
 git add -f
```

用户还可以使用清理被忽略文件的测试选项：`git clean -Xnd` 和底层（管道化）的命令 `git ls-files`：
```shell
$ git ls-files --others --ignored --exclude-standard
.DS_Store
```

# Git如何永久删除文件(包括历史记录)
本文复制于[Git如何永久删除文件(包括历史记录)](https://www.cnblogs.com/shines77/p/3460274.html)

有些时候不小心上传了一些敏感文件(例如密码), 或者不想上传的文件(没及时或忘了加到.gitignore里的),而且上传的文件又特别大的时候, 这将导致别人clone你的代码或下载zip包的时候也必须更新或下载这些无用的文件,
因此, 我们需要一个方法, 永久的删除这些文件(包括该文件的历史记录).  

首先, 可以参考 github 的帮助:
[https://help.github.com/articles/remove-sensitive-data](https://help.github.com/articles/remove-sensitive-data "https://help.github.com/articles/remove-sensitive-data")

## 步骤一: 从你的资料库中清除文件

以Windows下为例(Linux类似), 打开项目的Git Bash,使用命令:  

```bash
git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch path-to-your-remove-file' --prune-empty --tag-name-filter cat -- --all
```

其中, path-to-your-remove-file 就是你要删除的文件的相对路径(相对于git仓库的跟目录), 替换成你要删除的文件即可. 注意一点，这里的文件或文件夹，都不能以 '/' 开头，否则文件或文件夹会被认为是从 git 的安装目录开始。

如果你要删除的目标不是文件，而是文件夹，那么请在 `git rm --cached' 命令后面添加 -r 命令，表示递归的删除（子）文件夹和文件夹下的文件，类似于 `rm -rf` 命令。

此外，如果你要删除的文件很多, 可以写进一个.sh文件批量执行, 如果文件或路径里有中文, 由于MinGW或CygWin对中文路径设置比较麻烦, 你可以使用通配符`*`号, 例如: `sound/music_*.mp3`, 这样就把sound目录下以music_开头的mp3文件都删除了.

例如这样, 新建一个 bash 脚本文件，del-music-mp3.sh:
```bash
git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch projects/Moon.mp3' --prune-empty --tag-name-filter cat -- --all
git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch sound/Music_*.mp3' --prune-empty --tag-name-filter cat -- --all
```

 如果你看到类似下面这样的, 就说明删除成功了:
```
Rewrite 48dc599c80e20527ed902928085e7861e6b3cbe6 (266/266)
# Ref 'refs/heads/master' was rewritten
```


如果显示 xxxxx unchanged, 说明repo里没有找到该文件, 请检查路径和文件名是否正确.

注意: 补充一点, 如果你想以后也不会再上传这个文件或文件夹, 请把这个文件或文件夹添加到.gitignore文件里, 然后再push你的repo.

## 步骤二: 推送我们修改后的repo

以强制覆盖的方式推送你的repo, 命令如下:

```bash
git push origin master --force --all
```

这个过程其实是重新上传我们的repo, 比较耗时, 虽然跟删掉重新建一个repo有些类似, 但是好处是保留了原有的更新记录, 所以还是有些不同的. 如果你实在不在意这些更新记录, 也可以删掉重建, 两者也差不太多, 也许后者还更直观些.

执行结果类似下面:
```bash
Counting objects: 4669, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4352/4352), done.
Writing objects: 100% (4666/4666), 35.16 MiB | 51 KiB/s, done.
Total 4666 (delta 1361), reused 0 (delta 0)
To https://github.com/defunkt/github-gem.git
 + beb839d...81f21f3 master -> master (forced update)
```

为了能从打了 tag 的版本中也删除你所指定的文件或文件夹，您可以使用这样的命令来强制推送您的 Git tags：

```bash
git push origin master --force --tags
```

## 步骤三: 清理和回收空间

虽然上面我们已经删除了文件, 但是我们的repo里面仍然保留了这些objects, 等待垃圾回收(GC), 所以我们要用命令彻底清除它, 并收回空间.  

命令如下:
```bash
rm -rf .git/refs/original/
git reflog expire --expire=now --all
git gc --prune=now
```
输出：
```bash
Counting objects: 2437, done.
# Delta compression using up to 4 threads.
# Compressing objects: 100% (1378/1378), done.
# Writing objects: 100% (2437/2437), done.
# Total 2437 (delta 1461), reused 1802 (delta 1048) 
```
命令：
```
git gc --aggressive --prune=now
```
输出：
```bash
Counting objects: 2437, done.
# Delta compression using up to 4 threads.
# Compressing objects: 100% (2426/2426), done.
# Writing objects: 100% (2437/2437), done.
# Total 2437 (delta 1483), reused 0 (delta 0) 
```


参考自:

[http://whoop.sinaapp.com/blog/article/21](http://whoop.sinaapp.com/blog/article/21 "http://whoop.sinaapp.com/blog/article/21")

[http://blog.csdn.net/meteor1113/article/details/4407209](http://blog.csdn.net/meteor1113/article/details/4407209 "http://blog.csdn.net/meteor1113/article/details/4407209")



