---
title: vim 搜索和替换
tags:
  - vim
categories:
  - Tool
  - Editor
---
注意查找回车应当用 `\n`，而替换为回车应当用 `\r`（相当于 `<CR>`）。
[harttle - 在 Vim 中优雅地查找和替换](https://harttle.land/2016/08/08/vim-search-in-file.html)
[cooper - Vim查找替换及正则表达式的使用](https://tanqisen.github.io/blog/2013/01/13/vim-search-replace-regex/)
# search
vim 查找支持正则表达式

| key              | effect                                   |
| ---------------- | ---------------------------------------- |
| `/`              | 向下查找。`n` 查找下一个，`N` 查找上一个 |
| `/\<theme\>`     | 严格匹配 theme                           |
|                  | 如果你输入 "/the"，你也可能找到 "there"。要找到以 "the" 结尾的单词，可以用：  `/the\>` `\>` 是一个特殊的记号，表示只匹配单词末尾。类似地，`\<` 只匹配单词的开头。这样，要匹配一个完整的单词 "the"，只需：`/\<the\>` |
| `?`              | 向上查找。`?` 也就是 `shift` + `/`       |
| `q/`             | 查看查找历史                             |
| `q?`             | 查看向上查找历史                         |
| 后缀`\c`         | 大小写不敏感                             |
| 后缀`\C`         | 大小写敏感                               |
| `*`              | 查找光标所在单词                         |
| `g*`             | 查找光标所在字符序列                     |
| `:set incsearch` | 敲键时就高亮                             |
| `:set hlsearch`  | highlight all pattern matches            |

# substitute
`:s` command
`:[range]s[ubstitute]/{pattern}/{string}/[flags] [count]`
`:{作用范围}s/{目标}/{替换}/{替换标志}`

### range

| command             | effect                                                          |
| ------------------- | --------------------------------------------------------------- |
| 不填                | 当前行                                                          | 
| `:%s/foo/bar/g`     | 全文                                                            |
| `:'<,'>s/foo/bar/g` | 在 Visual 模式下选择区域后输入 `:`，Vim 即可自动补全为 `:'<,'>` |
| `:5,12s/foo/bar/g`  | 2-11行                                                          |
| `:.,+2s/foo/bar/g`  | 当前行与接下来两行                                              |

### flags

| flag | effect                                   |
| ---- | ---------------------------------------- |
| 不填 | 只替换从光标位置开始，目标的第一次出现   |
| `g`  | globle, 全局替换（即替换目标的所有出现） |
| `c`  | confirm, 替换前需要确认                  |
| i    | ignore, 忽略大小写                       |

```
replace with bar (y/n/a/q/l/^E/^Y)?
```

按下 `y` 表示替换，`n` 表示不替换，`a` 表示替换所有，`q` 表示退出查找模式， `l` 表示替换当前位置并退出。`^E` 与 `^Y` 是光标移动快捷键。

