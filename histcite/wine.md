# HistCite 在非 Windows 环境下的安装

## 1. 安装

Mac 系统

```sh
brew install wine --devel
```

Linux 系统，装上 wine 就可以，一般来说 wine-devel 功能强一些，稳定性也足够。

将 HistCite 的可执行文件放在 `~/.wine/dirve_C/Program Files/HistCite`，路径可自选，没有空格更方便。

> 建立wine的C盘的fakepath目录。
> `mkdir ~/.wine/dirve_C/fakepath`
> 或者链接。
> `ln -s "hsi文件备份目录" ~/.wine/dirve_C/fakepath`

## 2. 合并文件脚本

> **！注意**，以下脚本会合并 `~/Downloads` 下所有文件名为 `savedrecs*.txt` 的文件，使用前务必保证该文件夹内txt文件都是刚刚下载的。

```sh
#!/usr/bin/env bash
# conding:utf-8
echo "FN Thomson Reuters Web of Knowledge" > ~/.wine/drive_c/fakepath/histmerge.txt
echo 引文合并中...
IFS=$'\n'
for itxt in $(ls ~/Downloads/savedrecs*.txt | sed "s/[ ,(,)]/\\\&/g")
do
  eval $"tail -n +2 $itxt >> ~/.wine/drive_c/fakepath/histmerge.txt"
done
echo 引文已合并至 "~/.wine/drive_c/fakepath/histmerge.txt"
```

从 Web of Science 导出文件后，运行本脚本，即可更改格式，并将多个文件合并。

## to-do list

- [ ] 支持直接打开 hci 文件(貌似只在 win 上实现过，测试直接 wine 打开无反应，可能和 wine 的传参有关)。
- [ ] 检索，合并结果的自动化，更多网站的兼容。
