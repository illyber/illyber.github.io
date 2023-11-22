---
title: Vscode notes
tags: vscode
categories:
  - Tool
  - Editor
---

# vscode安装和配置

## 安装vscode

1. 安装curl

```bash
sudo apt install curl
```

2. 用 curl 导入 Microsoft GPG 公钥：

```bash
curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
```

一旦成功，这个命令将会返回OK.

3. 添加 Visual Studio Code 软件源

```bash
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
```

4. 安装 Visual Studio Code 软件包：

```bash
sudo apt update
sudo apt install code
```

5. 如发生错误，可尝试安装下列依赖包

```bash
sudo apt install software-properties-common apt-transport-https
```

## vscode 插件

- chinese
- C/C++
- code runner
- open in default browser
- htmltagwrap
- auto rename tag
- open in default browser
- markdown all in one
- markdown preview github styling
- path intellisense
- vscode-icons
- wsl
- ShellCheck
- live server

## 字体大小

可直接复制配置文件。

1. 编辑器字体大小：右下角齿轮->设置->搜索字体->Editor:Font Sizer 里写上18

![](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281946417.png)

2. 系统界面缩放。在设置里搜索「缩放」

   ![image-20221007185204895](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281946418.png)

3. 终端字体大小：在设置里搜索 Terminal › Integrated: Font Size

![image-20221007191235961](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281946419.png)

## 调试程序

1. 新建名为 test 的文件夹作为工作区
2. 在test文件夹里可写test.c源文件
3. 新建 .vscode 文件夹，不要省略 '.'
4. 在 .vscode 文件夹里新建launch.json,填写下面

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "C/C++",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}/${fileBasenameNoExtension}",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "preLaunchTask": "compile",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        }
    ]
}
```

5. 在.vscode 文件夹里新建task.json，填写下面

```json
{
    "version": "2.0.0",
    "tasks": [{
            "label": "compile",
            "command": "gcc",
            "args": [
                "-g",
                "${fileBasenameNoExtension}*.c",
                "-lm",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
            "problemMatcher": {
                "owner": "cpp",
                "fileLocation": [
                    "relative",
                    "${workspaceRoot}"
                ],
                "pattern": {
                    "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning|error):\\s+(.*)$",
                    "file": 1,
                    "line": 2,
                    "column": 3,
                    "severity": 4,
                    "message": 5
                }
            },
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```

## code runner 设置

1. 清除先前的运行记录
   ![](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281946420.png)
2. 在底部终端输出/输入结果
   ![](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281946421.png)
3. 编译多个源文件
code runner扩展设置->Executor Map->在 settings.json 中编辑
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202308030335293.png)
```json
将
"c": "cd $dir && gcc $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
改成
"c": "cd $dir && gcc $fileNameWithoutExt*.c -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
```


## vscode 模板

[VScode中创建你的代码模板](https://zhuanlan.zhihu.com/p/100504877)

# 技巧

- `!+tab` or `!+enter`. 建立框架
- `Ctrl + d`. 同时选中改变多个
- 查看->自动换行. 可使较长的代码自动换行
- `ctrl+enter`;`ctrl+shift+enter`分别是另外开一行到下一行和上一行
- `li*5直接生成5行li`
- 安装htmltagwrap. 自动更改两侧标签, `alt+w`, 在选中的文本的两端添加标签
- 注释: `Ctrl+/`

# 移动光标
- 快速移到右边按`end(fn+->)`

# 折叠代码
- 折叠所有代码：`ctrl+k, ctrl_0`

# 整行移动
```
alt+up/alt+down
缩进. 用光标选中+`tab`
取消缩进. 用光标选中+`shift+tab`
```

# 删除一行
```
ctrl+shift+k
```
# 新建一行
```
ctrl+enter
```
# 特殊符号
```
∨∧∩∪
## 向下取整
$\lfloor x \rfloor$

## 向上取整
$\lceil x \rceil$

≤ \leq
≥ \geq
×
```
省略号及其示意图：
`\dots, \cdots, \vdots, \ddots`
$$\dots, \cdots, \vdots, \ddots$$
乘号：
`\cdot, \bullet, \times`
$$\cdot, \bullet, \times$$

# 多光标
- `alt` + 鼠标左键选择。
- `F2`. 选中变量后重命名多个变量。
- alt+shift+鼠标拖动. 列选择/方块选择
# 输入联想
- 要输入多个关键词，只需输入每个词的开头

# Emmet 语法
- vscode 自带的工具
- 快速输入代码
- 语法类似上面的选择器
- [emmet语法简介](https://www.bilibili.com/video/BV1Kg411T7t9?p=71&vd_source=4f8ddad44fd904574089cafb91e9e009)
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202308021119925.png)

| 效果               | 输入        | 显示                               | 备注               |
| ------------------ | ----------- | ---------------------------------- | ------------------ |
| 缩写               | ff          | `font-family: ;`                   | 不一定要用首字母   | 
|                    | fz          | `font-size: ;`                     |                    |
| 带类名的标签       | p.box       | `<p class="dox"></p>`              | 省略标签时默认 div |
| 带id的标签         | p#box       | `<p id="box"></p>`                 |                    |
| 带类名和id         | p.red#one   | `<p class="red" id="one"></p>`     |                    |
| 创建同级标签       | p+div       | `<p></p> <div></div>`              |                    |
| 创建嵌套标签       | div>p       | `<div><p></p></div>`               |                    |
| 创建多层嵌套       | `div>p*3`   | `<div><p><p><p></p></p></p></div>` |                    |
| 创建包含文本的嵌套 | div>p{text} | `<div><p>text</p></div>`           |                    |

数字递增：
```html
ul>li{$}*3

<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
</ul>
```