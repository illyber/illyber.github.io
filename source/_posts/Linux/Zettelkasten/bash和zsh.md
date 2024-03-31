2024 0331 16:06
Tags: #bash	#zsh

---

# bash 快捷键
## 说明
参考 [harttle - Bash 快捷键](https://harttle.land/2015/11/09/bash-shortcuts.html#)

[Bash](http://www.gnu.org/software/bash/)快捷键其实是[GNU Readline](http://tiswww.case.edu/php/chet/readline/rltop.html)快捷键， [GNU Readline Library](http://tiswww.case.edu/php/chet/readline/rltop.html)是一个来接受用户输入的GNU软件包。 它是包括[Bash](http://www.gnu.org/software/bash/)在内的绝大多数Shell的底层库， 甚至OSX/Windows/Linux下的绝大多数软件都采用与之兼容快捷键。 因此这些快捷键可以在很大程度上支持纯键盘操作，尤其是在Linux/OSX下。

## 示意图

![bash-shortcut](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202302131024902.webp)

## 光标移动

|   快捷键    |             描述             |
| :---------: | :--------------------------: |
| `Ctrl + a`  |        移动光标到行首        |
| `Ctrl + e`  |        移动光标到行尾        |
|  `Alt + f`  | 移动光标前进一个单词（词首） |
|  `Alt + b`  | 移动光标后退一个单词（词首） |
| `Ctrl + f`  |       光标前进一个字母       |
| `Ctrl + b`  |       光标后退一个字母       |
| `Ctrl + xx` |  当前位置与行首之间光标切换  |

## 剪切粘贴

行尾为前，行首为后。

|   快捷键   |            描述            |
| :--------: | :------------------------: |
| `Ctrl + k` |      删除从光标到行尾      |
| `Ctrl + u` |      删除从光标到行首      |
|            |                            |
| `Alt + d`  |   从光标向前删除一个单词   |
| `Ctrl + w` |   从光标向后删除一个单词   |
|            |                            |
| `Ctrl + d` |     删除光标前一个字母     |
| `Ctrl + h` |     删除光标后一个字母     |
|            |                            |
| `Alt + t`  | swap(当前单词, 上一个单词) |
| `Ctrl + t` | swap(当前字母, 上一个字母) |
|            |                            |
| `Ctrl + y` |    粘贴上一次删除的文本    |

## 大小写转换

|  快捷键   |               描述               |
| :-------: | :------------------------------: |
| `Alt + c` | 大写当前字母，并移动光标到单词尾 |
| `Alt + u` |       大写从当光标到单词尾       |
| `Alt + l` |       小写从当光标到单词尾       |

## 历史命令

|   快捷键   |           描述           |
| :--------: | :----------------------: |
| `Ctrl + r` |     向后搜索历史命令     |
| `Ctrl + g` |         退出搜索         |
| `Ctrl + p` |     历史中上一个命令     |
| `Ctrl + n` |     历史中下一个命令     |
| `Alt + .`  | 上一个命令的最后一个单词 |

## 终端指令

|   快捷键   |                 描述                  |
| :--------: | :-----------------------------------: |
| `Ctrl + l` |                 清屏                  |
| `Ctrl + s` | 停止输出（在Zsh中为向前搜索历史命令） |
| `Ctrl + q` |               继续输出                |
| `Ctrl + c` |             终止当前命令              |
| `Ctrl + z` |             挂起当前命令              |
| `Ctrl + d` |        结束输入（产生一个EOF）        |

## 纯键盘写邮件

绝大多数操作系统（OSX，Windows，Linux）中的绝大多数软件（GUI的、命令行的） 在底层都使用GNU Readline兼容的库来读取用户输入。 **因此Bash快捷键完全可以胜任纯键盘写邮件**：

- 同一行内移动光标：`Ctrl-B`, `Ctrl-F`, `Ctrl-A`, `Ctrl-E`等。
- 上下行移动光标：`Ctrl-P`, `Ctrl-N`。
- 剪切/粘贴：`Ctrl-W`, `Alt-D`等。

# echo 显示颜色
参考：[kgkdfgjdfgdf - 真 ● 禁秘技 ● 奥义 ● 终端美化](https://zhuanlan.zhihu.com/p/268461410), [yfeng - shell echo 显示颜色](https://zhuanlan.zhihu.com/p/181609730)

## 显示所有颜色
```bash
for i in {0..255};
    do print -Pn "%K{$i}  %k%F{$i}${(l:3::0:)i}%f " ${${(M)$((i%6)):#3}:+$'\n'};
done
```

## 命令格式
```shell
echo -e "\033[字背景颜色;字体颜色;字体属性m 需要输出的内容 \033[0m"
```
- `\033` 转义起始符，定义一个转义序列，可以使用 `\e` 或 `\E` 代替。
- `[` 表示开始定义颜色。
- `字背景颜色` 范围 `40-47` 。
- `字体颜色` 范围 `30-37` 。
- `字体属性`
- `m` 转义终止符，表示颜色定义完毕。
- 再次使用 `\033[` ，表示再次开启颜色定义，`0` 表示颜色定义结束，所以 `\033[0m` 的作用是恢复之前的配色方案。

## 背景颜色
背景颜色：40-47
- 默认=0
- 黑色=40
- 红色=41
- 绿色=42
- 黄色=43
- 蓝色=44
- 紫色=45
- 天蓝色（青色）=46
- 白色=47
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307232050999.png)


## 字体颜色
字体颜色：30-37
- 默认=0
- 黑色=30
- 红色=31
- 绿色=32
- 黄色=33
- 蓝色=34
- 紫色=35
- 天蓝色（青色）=36
- 白色=37
颜色示例：
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307232046464.png)

## 字体控制选项
- `\e[0m` 关闭所有属性
- `\e[1m` 设置高亮度
- `\e[4m` 下划线
- `\e[5m` 闪烁
- `\e[7m` 反显，撞色显示，显示为白字黑底，或者显示为黑底白字
- `\e[8m` 消影，字符颜色将会与背景颜色相同
- `\e[nA` 光标上移 n 行
- `\e[nB` 光标下移 n 行
- `\e[nC` 光标右移 n 行
- `\e[nD` 光标左移 n 行
- `\e[y;xH` 设置光标位置
- `\e[2J` 清屏
- `\e[K` 清除从光标到行尾的内容
- `\e[s` 保存光标位置
- `\e[u` 恢复光标位置
- `\e[?25` 隐藏光标
- `\e[?25h` 显示光标

# Zsh 快捷键
显示所有快捷键：`bindkey -L`

即zsh line editor
与 gnu readline library 不一致的快捷键：

| 快捷键   | zle        | readline             |
| -------- | ---------- | -------------------- |
| `ctrl+u` | 删除一整行 | 删除光标到行首的内容 | 

# 运行zsh初始设置

```zsh
autoload -Uz zsh-newuser-install
zsh-newuser-install -f
```

补全一个单词：`alt+f`. 设计得和gnu readline一致

# zsh插件和主题

```shell
autojump
antigen use prezto
antigen bundle rupa/z
antigen bundle Vifon/deer
antigen bundle zdharma-continuum/fast-syntax-highlighting
antigen bundle zsh-users/zsh-autosuggestions
antigen bundle willghatch/zsh-cdr
antigen bundle zsh-users/zaw
zsh-users/zsh-completions

antigen theme romkatv/powerlevel10k

antigen apply
```

## zsh-autosuggestions

[A Guide to the Zsh Line Editor with Examples](https://thevaluable.dev/zsh-line-editor-configuration-mouseless/)

- `^` - Represent the `CTRL` key. For example: `^c` for `CTRL+c`.
- `\e` - Represent the `ALT` key. For example: `\ec` for `ALT+c`.

# zsh 提示符
参考：[布_鲁斯 - zsh 命令提示符 PROMPT](https://www.cnblogs.com/b-ruce/p/5851624.html), [木_穆 - 自定义 zsh 提示（配置PROMPT或PS1）](https://www.jianshu.com/p/dcf39bc7821a)

在 `~/.zshrc` 里设置

例子：`export PROMPT='%B%F{green}%n@%M%f%b:%B%F{blue}%/%f%b$ '`

```.zshrc
%%  一个'%'
#%) 一个')'

%y  当前的tty名
%l  当前的tty名，如 pts/1

%M  完整主机名
%m  主机名（在第一个句号之前截断）
%n  当前用户名

%. %c %C 前两个显示相对路径的当前文件夹名，最后一个是绝对路径（也就是说，前两个在家目录下显示'~'，最后那个显示你的用户名），'%'后的数字表示显示几层路径
%/ %d   显示当前工作路径（$pwd）。如果'％'后面是一个整数，它指定显示路径的元件的数量;没有数字就显示整个路径。一个负整数就是指定主目录，即％-1d代表第一部分
%~  目前的工作目录相对于～的相对路径
```

- `%F{color}` 是配置颜色，{}中color是 256 色的颜色值，也可以使用`black，red，green，yellow，blue，magenta，cyan和white`等常用色。
- `%f` 表示后面恢复默认颜色。
- `%B` 粗体 。
- `%b` 表示后面恢复默认子重。
## `${(%):-%N}`
[${(%):-%N}](https://stackoverflow.com/questions/74822753/why-n-to-get-expansion-of-escapes-in-zsh?rq=3)






---
