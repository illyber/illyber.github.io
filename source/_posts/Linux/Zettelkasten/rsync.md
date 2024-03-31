2024 0331 15:59
Tags: #传输文件

---

remote sync
适用于大文件和跨文件系统传输，和远程传输。
```shell
rsync -P source destination
```
`-P` 与 `--partial --progress` 选项的作用是相同的，该选项使得文件可以分块传输并显示传输过程中的进度。
`-r`/`--recursive` 递归到目录中传输。

目录斜杠遵循unix约定

`rsync -Pr ~/Videos/学习视频/ .`: 复制目录里的内容，不复制目录名。

`rsync -Pr ~/Videos/学习视频 .` 复制目录名，并复制目录内容。这样理解，/usr 就代表了一个目录整体。

**rsync 将包含大量小文件的本地文件夹移动到另一个磁盘中：**
rsync -avh --progress /path/to/source/folder /path/to/destination/folder 

或者清爽版：

rsync -av /path/to/source/folder /path/to/destination/folder 

在上述命令中，你需要替换 `/path/to/source/folder` 为源文件夹的路径，将 `/path/to/destination/folder` 替换为目标文件夹的路径。

命令参数说明：

- `-a`：启用归档模式，保留文件的权限、时间戳等属性。
- `-v`：显示详细输出，以便查看复制过程中的进度和详细信息。
- `-h`：以人类可读的格式显示文件大小和进度。
- `--progress`：显示复制的进度。




---
