# Zotero 开箱指南

> Zotero /zoʊˈtɛroʊ/ 是一款免费易用工具，用来帮助你收集，整理，引用，分享研究资料。

作为一款优秀开源文献管理软件软件，Zotero 自身功能不俗，且拥有丰富的扩展，能满足更多人的不同需求。

> 本文简述了安装和初始设定的必要设置，多数链接均指向官网文档。官方文档虽略显过时，但内容详尽且极少错误。希望有志之士贡献翻译[Zotero Wiki](https://www.zotero.org/support/?do=login)

## 安装

Zotero 分为两个部分，即独立版及浏览器插件。

- 独立版：软件主体，承载了绝大多数功能
- 浏览器插件：将文献从网页收录到独立版内

打开[下载链接](https://www.zotero.org/downloads)，页面左侧为独立版，右侧为浏览器插件，按常规下载安装即可。

> - 独立版支持: Windows, Mac, Linux
>   Mac 可用`brew cask`安装
>   Linux 下载后直接运行可执行文件，亦可通过收录源安装，此处不再赘述
> - 浏览器支持: Chrome, Firefox, Safari
>   浏览器的选择：
>   - Chrome: 最快，但需要科学上网
>   - Fireworks & Safari: 网速慢对插件收录影响较大

## 初始设定

1. 修改`数据存储位置`(建议所有系统修改，对 Windows 尤为重要)

    > `数据存储位置`是 Zotero 本地几乎所有的配置、文献数据库、插件数据库以及附件存放的地方。该目录下的`storage`子目录，存放有本地所有`文件`类型的附件。

    选择`首选项`→`高级`→`文件和文件夹`中的`数据存储位置`。
    点选`自定义`，改为自己顺手的位置(Windows 建议挪出 C 盘)。

    > 建议 Windows 上将数据存储位置挪出 C 盘，避免重装系统造成的文献配置丢失。
    > 修改后 Zotero 会询问重启，绝大多数配置会丢失，因此应首先修改。

    ![设置同步根目录](figs/sync_root_folder.png)

1. 设置同步账户并取消内置附件同步

    [注册 Zotero 账户](https://www.zotero.org/user/register/)，在`首选项`→`同步`→`设置`中填写账号密码。

    > 注册过程含 Google 人机验证，须科学上网。

    取消`首选项`→`同步`→`设置`中`文件同步`下面两个选项的勾选。

    > Zotero 免费账户仅含300Mb 空间，且仅用于同步附件，故取消内置文件同步。

    ![同步设置](figs/cancel_sync_attachments.png)

    想获得更多空间，以及更灵活的方案，参考[附件同步](sync.md)。

1. 取消自动生成快照

    在`首选项`→`常规`取消自动生成快照。

    > 快照: 离线网页
    > 快照可读性差异大，且包含大量零散文件。
    > 可读性好的网页，可手动保存快照。

    ![取消快照](figs/cancel_auto_snapshot.png)

## 文献迁移

[通用](https://www.zotero.org/support/kb/importing)
[自 Endnote 迁移](https://www.zotero.org/support/zh/kb/importing_records_from_endnote)
[自 Citavi 迁移](https://www.zotero.org/support/kb/import-from-citavi)

## 使用简介

[快速入门](https://www.zotero.org/support/zh/quick_start_guide)

> 阅读安装以后内容，快速了解 zotero 的功能与使用方法

[题录收录](https://www.zotero.org/support/zh/getting_stuff_into_your_library)

[Word 插文献](https://www.zotero.org/support/word_processor_plugin_usage)
[Word 插文献(经典模式)](https://www.zotero.org/support/word_processor_plugin_usage_classic)

[引文样式](https://www.zotero.org/support/zh/styles)
[修改样式](https://www.zotero.org/support/dev/citation_styles)

## 插件扩展

[ZotFile](http://zotfile.com/)
[Zotero Better Bib(La)Tex](https://retorque.re/zotero-better-bibtex/)
[Zutilo Utility for Zotero](https://github.com/willsALMANJ/Zutilo)
[ZoteroQuickLook](https://github.com/mronkko/ZoteroQuickLook)
