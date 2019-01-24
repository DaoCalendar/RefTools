# Spacemacs 一款鳌拜会选的 LaTeX IDE？！

> 当因为各种原因，你最终需要选 {Vim/Emacs} 作为你的 LaTeX 编辑器的时候，小心了，你面临的是一个让人能打起来的问题。但是，你其实可以微微一笑，道出：“小孩子才做选择题，而我选择都(all)要(buy)！”

Spacemacs 是一款整合 Vim 和 Emacs 使用习惯的 Emacs 配置，它以最好的编辑器既不是 Vim 也不是 Emacs 而是二者的合体为标语，颇有鳌拜大人的风范。本文主要旨在利用 Spacemacs 在 macOS/Linux 平台，配置实现快速编辑预览支持拼写检查和纠错的 LaTeX 编辑器。

> 不是 Windows 平台不能配置，而是 Windows 平台比 macOS 的坑更多，粗略配置完后还是较其余两个平台有差距，没更多时间和心情去踩 Windows 的坑了，Windows 的用户需要自力更生或者选择包括 VSCode 在内的其他编辑器。

在某些开发大神看来，Spacemacs 配置起来已经简单的不的了，但是笔者仍需提醒，Spacemacs 适用的是折腾能力较强，喜欢纯键盘操作多过键盘鼠标操作，对编辑器有较高的自定义需求的人群。当你选择了 Spacemacs 时候，意味着你最好熟悉类 Linux 终端及 shell 的基本操作，以及入门级别的`git`使用能力。

> 除此之外，本文并不是一步一截图的苦口婆心式教程，而是笔者配置过程中，遇到不太好找答案的几个问题的解决方案，它同时也不能帮你入门 Spacemacs，所以，目标不太一致的朋友们，看到这里，就可以停止不浪费余下的几分钟了。

## Spacemacs 的安装

照例，官方有讲，我不废话。[官网](http://spacemacs.org/) [开发主页](https://github.com/syl20bnr/spacemacs)

本文的所有配置如无特殊说明，均为对 Spacemacs 的高级配置文件 `$HOME/.Spacemacs` 的修改。

入门的快捷键，建议大家搜索 `Spacemacs Cheat Sheet`然后进行熟悉。

## [可选] emacsclient 的配置

通过 deamon 模式跑一个 `emacs` 服务器，然后 `emacsclient` 去连接这个服务器，会感觉 `emacs` 是秒开的，并且保存 `emacs`的编辑状态。这虽然不是必须的，但真心觉得配置了方便。

### Linux

对于 Linux 以 Archlinux 为例，只需要在 `$HOME/.local/share/applications/` 目录中新建 `emacsclient.desktop`即可，内容建议:

```conf
[Desktop Entry]
Name=Emacs Client
GenericName=Text Editor
Comment=Edit text
MimeType=text/english;text/plain;text/x-makefile;text/x-c++hdr;text/x-c++src;text/x-chdr;text/x-csrc;text/x-java;text/x-moc;text/x-pascal;text/x-tcl;text/x-tex;application/x-shellscript;text/x-c;text/x-c++;
Exec=emacsclient -ca '' %F
Icon=emacs
Type=Application
Terminal=false
Categories=Development;TextEditor;
StartupWMClass=Emacs
Keywords=Text;Editor;
```

* [ ] 如果有必要，以后补充一个 shell 内 `emacsclient` 的 alias/function 。

### macOS

> macOS 么，一般不那么 geek 的人都想要个图形界面启动的方式（.app）。
>
> 于是，我一开始的方案是 homebrew 里的 service 自启 + Automator 封装脚本为 "Emacs Client.app"，但是这样会让 LaTeX layer 找不到 `latexmk` 而无法编译。
>
> 原因在于 macOS 通过 `launchctl` 自启动的话，`$PATH` 环境变量默认为空。

经过一番折腾，最终我选择了，不跑 service 直接通过 "Emacs Client.app" 来启动服务，稍微有点不优雅的就是第一次打开 "Emacs Client.app" 需要跑2次，但也比去终端里重启 homebrew 的 service 要方便也快得多了。

打开 Automator，新建文稿，应用程序，运行 Shell 脚本。

> 此处以`emacs`及`emacsclient`都从`/usr/local/bin`目录下直接访问为例，实际填写时，请以自己机器上的绝对路径为准。

* Shell: `/bin/sh`
* 传递输入: 作为自变量
* `/usr/local/bin/emacsclient -nca "/usr/local/bin/emacs --daemon" -- "$@" >/dev/null 2>&1`

> 包括 Linux 系统的 desktop，参数的意义建议看下 `man emacsclient`
>
> macOS 将输出传到 `/dev/null` 是有意义的，否则 app 文件的体积会不断增大。

保存为 `~/Applications/Emacs Client.app` 后，是小机器人（Automator 默认）图标，没关系，选中 "Emacs Client.app" 按 ⌘ + i 键（或者右键显示简介），将 Emacs 的图标拖到左上角小机器人上，即可完成替换。

> 更多方案，可见我[在 Emacs-China 的自问自答](https://emacs-china.org/t/macos-emacs-latex-emacs-client-latexmk/7996)。

## LaTeX layer

基本配置及使用见 [开发主页 - LaTaX layer](https://github.com/syl20bnr/spacemacs/tree/master/layers/%2Blang/latex)

但是 macOS 会遇到一个每次启动重装 `auctex-latexmk` 的 bug(见 [spacemacs#10659](https://github.com/syl20bnr/spacemacs/issues/10659))，所以需要在 `dotspacemacs-configuration-layers` 为 LaTeX layer 增加变量

```lisp
  (latex :variables latex-build-command "LatexMk")
```

为不同平台配置 viewer，以 macOS 使用 Skim.app 的 `displayline`，linux 系统使用 Okular 为例。

> 现在基本不用定义 TeX-view-program-list 常用的都已经被[AUCTeX 内置](http://git.savannah.gnu.org/cgit/auctex.git/tree/tex.el#n1237)

在 `defun dotspacemacs/user-config` 添加

```lisp
  (cond
   ((spacemacs/system-is-mac) (setq TeX-view-program-selection '((output-pdf "displayline"))))
   ((spacemacs/system-is-linux) (setq TeX-view-program-selection '((output-pdf "Okular")))))
  )
```

macOS 支持正反搜索的软件并不多，Skim.app 是其中之一，但是和 emacs 无法找到 `latexmk` 一样，现在的 macOS 中，需要在 选项 -> 同步中，先选择 emacs，然后再切换为自定义，将 `emacsclient` 路径改为完整路径。

## Spell Checker layer

基本配置及使用见 [开发主页 - Spell Check layer](https://github.com/syl20bnr/spacemacs/tree/master/layers/%2Bcheckers/spell-checking)

> macOS 没法默认使用 `aspell`，如果 macOS 下使用 `aspell` 需要设置 ispell-program-name。
> 当 shell 内的 $LANG 变量不为 en_US(或者其他英语 locale) 时，最好设置 ispell 的默认词典为 english，插件的自动语言检测尤其在 client 模式下不好用。

在 `defun dotspacemacs/user-config` 添加

```lisp
  (with-eval-after-load "ispell"
   (setq ispell-program-name "aspell")
   (setq ispell-dictionary "english"))
```

## 自定义编译

修改文本末尾的注释通过 `AUCTeX` 来实现自定义编译，会比直接编辑器配置来的直接方便。本部分所提及自定义注释应该添加到文档末尾，且包含在以下内容之内。

```tex
%%% Local Variables:
%%% mode: latex
%%% coding: utf-8
需要增加的自定义内容
%%% End:
```

### 主/从文档

从文档

```tex
%%% TeX-master: 主文档相对/绝对路径，不包含后缀(tex)
```

主文档

```tex

%%% TeX-master: t
```

### 自定义编辑引擎，附加参数(以实现`xelatex`为例)

在需要编辑(发起编译)的 tex 文档中加入

> 无论是主文档或者从文档，只要需要从该文档发起编译，都应添加。

```tex
%%% TeX-engine: xetex
%%% TeX-command-extra-options: "-shell-escape"
```

更多附加参数请参考 [AUCTeX 4.1.3 Options for TeX Processors](https://www.gnu.org/software/auctex/manual/auctex/Processor-Options.html)

## 结语

本文虽然不是一步一截图风格的教程，但个人看来是官方文档的一个较好补充，基本配置需要修改的部分已经完全包含在文中了，链接更多是为了学习使用。

当按照本文所述将以上两个 layer 配置好后，就能获得一个非常便捷好用的 LaTeX 编辑器了，编辑文本的习惯和 Vim 一致(如果 Spacemacs 初始化的时候，都选择默认)，而快捷键则是由 Spacemacs 定制，可谓空格之内，4键可达。尤其当你使用 `git` 来管理的 latex project 时，这些优势更加突出。

本人的 Spacemacs/Emacs/Vim 为入门级，配置目的是能用，力争好用，且 Emacs 还是蛮复杂的东西。所以望各位读者遇到问题，能够高台贵手，放过我，多求助于搜索引擎。这篇类似附加材料的东西，能博配置过 LaTeX layer 的大大们一笑足矣。
