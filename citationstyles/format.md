# 四步实现自定义 Zotero 参考文献格式

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=3 orderedList=false} -->
<!-- code_chunk_output -->

* [1. 区分 citation 与 bibliography](#1-区分-citation-与-bibliography)
* [2. 参考文献索引的格式化](#2-参考文献索引的格式化)
* [3. 参考文献书目的格式化](#3-参考文献书目的格式化)
	* [3.1 Zotero 的题目(title)字段](#31-zotero-的题目title字段)
	* [3.2 CSL 文件的使用及修改](#32-csl-文件的使用及修改)
	* [3.3 Word 插件中使用书目编辑器](#33-word-插件中使用书目编辑器)
	* [3.4 Word 中的"书目"样式](#34-word-中的书目样式)
	* [3.5 补缺的黑科技](#35-补缺的黑科技)

<!-- /code_chunk_output -->

> 基于 CSL 语言的参考文献管理软件，对参考文献书目格式的控制方法。本文所述同样适用于 Mendeley, Docear 等软件，但具体功能实现方式略有差异，需读者自行摸索。

对大多数人而言，"插文献"是使用文献管理软件的主要乃至唯一的作用，那"插文献"究竟指什么呢？

用**简洁，单一**的方式，满足学位论文，期刊杂志，出版书籍中，**种类繁复，格式复杂的参考文献及书目的要求**。

本文以 Zotero 为例，介绍了现在"流行的"文献管理软件，自定义 Microsoft-Word(后简称 Word ) 中参考文献书目及索引格式的方法，作用范围及顺序。本文中，简述了 citation 格式调整技巧，按照其人们日常的使用习惯及作用顺序，介绍了自定义 bibliography 的四种方法，也就是题目中所指『四步』。而 bibliograhpy 的第5部分，针对当前基于 CSL 工具无法处理好"et al."和"等"，提出了一些补救的方法，其中包括[自定义宏批量修改 CSL 生成参考文献书目的错误](fix_csl_gbt7714.md)。

> "流行的"指的是以 Citation Style Language (CSL)为基础的一类参考文献软件，相对经典的 EndNote 而言，Zotero, Mendeley, Docear 等软件均属于此类。
> Citation Style Language 是一种基于 XML 的广泛使用的开源语言，用于定义 citation 和 bibliography 的格式。
> CSL 主页 <http://citationstyles.org/>
> Zotero citation styles 介绍 <https://www.zotero.org/support/zh/dev/citation_styles>


## 1. 区分 citation 与 bibliography

> 两个单词差这么多，居然要我分清？！

看英文单词，他们长得完全不一样，但在中文语境中，一般都会被称为『参考文献』。为了区分二者，在后文中做出如下规定：

称 citation 为**参考文献索引**，或简称**索引**。它就是正文中的[1~3,5]或者 somebody (year)这样的东西。

> 索引，告诉读者正文的那些内容引用了哪些文献，即交代内容与引文的对应关系。

称 bibliography 为**参考文献书目**，或简称**书目**。它就是正文后，"References"或者"参考文献"部分的内容。这部分一般包括了被引文献的作者，年，期刊或出版社，[DOI](https://www.doi.org/)，[ISBN](https://zh.wikipedia.org/zh-cn/%E5%9B%BD%E9%99%85%E6%A0%87%E5%87%86%E4%B9%A6%E5%8F%B7)以及卷，期，页码等信息。

> 书目对被引文献做出了足够详尽的描述，能够帮助读者精确的锁定被引文献。

## 2. 参考文献索引的格式化

常见索引只有两种格式：数字 (number) 与作者-年代 (author-year)，这也是 CSL 的一种分类的方式。

但是，对于作者年代格式，需要多交代一句，一般使用作者年格式的期刊均有这样的要求：

- 句子中提到某个人时(即人名充当句子主谓成分时)，索引写做 author(year)；
- 引文对整个句子解释时(即人名不充当句子主谓成分时)，索引写做(author year)。

本文建议的处理是，在 Word 的 Zotero 选项卡中，点击"Add/Edit Citation"![](https://www.zotero.org/support/_media/word_integration/zotero-toolbar-word-add-edit-citation-5.png?w=16&cache=nocache&tok=a54d12)。在弹出的索引编辑器中勾选

![索引编辑器](https://www.zotero.org/support/_media/word_integration/edit_citation.png?cache=nocache)

- [x] `略去作者`/`Suppres Author`

于是生成一个 (year) 格式的索引，author 则直接写入正文。

## 3. 参考文献书目的格式化

书目的格式化，尤其是 CSL 文件的修改，由于较为复杂不再此处展开，将来会补充优秀教程链接或者单开一篇。

书目的格式化，按照 2 个层次，推荐 4 种方法给大家，建议顺序使用。

- 内容+字体格式
  - Zotero 的题目(title)字段
  - CSL 文件的使用及修改
  - Word 插件中使用书目编辑器
- 段落样式
  - Word "书目"样式

### 3.1 Zotero 的题目(title)字段

可以插入 html 语言的标签来达到给 title 字体格式的效果，一般用于化学/数学式中的上下角标，效果如下：

- `稳重的题目<sup>上标</sup>` 效果: 稳重的题目<sup>上标</sup>

- `积极的题目<sub>下标</sub>` 效果: 积极的题目<sub>下标</sub>

- `正经的题目<i>斜体</i>` 效果: 正经的题目<i>斜体</i>

下划线及粗体都也是 html 标签支持的，但一般来说，没有必要。

> 标题的修改仅限于零星特殊格式的字符，主要格式控制在 CSL 文件

### 3.2 CSL 文件的使用及修改

CSL 文件在整个书目格式化的过程中，占据最主要的地位。简而言之，它定义了 2 个东西。

- 书目的组成与先后顺序
- 书目各组成的字体格式
  - 字体格式主要包括，上下标，粗斜体，以及不同规则字母大写

Citation style language 在线数据库有大量预定义的格式(本文写作时，zotero 库中有 8192 种格式)，可以通过 Zotero 首选项直接安装，且现有的格式可以满足绝大多数需求。

对于已经安装好的 CSL 格式，在 Word 插件中点击 `Document Preferences` 可以应用或更换。

但当无法找到合适的格式文件时，可以选择修改现有的格式，具体的过程与方法，不在此展开。新手编辑 CSL 文件，建议使用 <http://editor.citationstyles.org> 的`Visual editor`。

> [Onlie Visul Editor 使用指南](https://github.com/citation-style-language/CSL-editor/wiki/User-guide-for-the-CSL-Editor)

### 3.3 Word 插件中使用书目编辑器

不论由于什么原因，通过前两种方法始终都无法获得想要的字体格式，那么应该选择使用 Word 中的插件中的书目编辑器，而不是手动改。

> 喜欢手改的人，在评论区讲出你的故事。

### 3.4 Word 中的"书目"样式

至此，我们已经彻底搞定了书目的内容和字体格式(注意，字体格式中并未包括字体大小)。那么，书目的字体大小，缩进，行间距由谁控制？

Word 中参考文献书目应用了 `书目`(Mac 与英文环境或为`Bibliography`)样式，可以尝试使用`Ctrl/Cmd` + `Shift` + `Alt` + `S`呼出样式窗口，编辑其中的段落样式，保存后刷新书目，参考文献书目段落样式将更新为你修改后的"书目"，且不随刷新失效。

> [微软：编辑样式](https://support.office.com/zh-cn/article/%E5%BA%94%E7%94%A8%E3%80%81%E6%9B%B4%E6%94%B9%E3%80%81%E5%88%9B%E5%BB%BA%E6%88%96%E5%88%A0%E9%99%A4%E6%A0%B7%E5%BC%8F-1a2cead9-897f-48a7-9122-7849d3b5030a)
> 清除缩进后缩进依旧不正确的，尝试删除书目中所有的制表位[微软：编辑制表位](https://support.office.com/zh-cn/article/%E8%AE%BE%E7%BD%AE%E3%80%81-%E6%B8%85%E9%99%A4%EF%BC%8C%E6%88%96%E5%88%A0%E9%99%A4%E5%88%B6%E8%A1%A8%E4%BD%8D-06969e0f-2c81-4fe0-8df5-88f18087a8e0)。

### 3.5 补缺的黑科技

至今，CSL 对 GB/T 7714 这种根据文献国别来确定 "等" 与 "et al" 的引文标准还没有很好的支持，（有一个 CSL 的补丁版本 Juris-M/jm-styles ，但是用户太少，而且需要专门客户端）。笔者建议解决 "等" 与 "et al" 这个问题，请参考。

[Zotero 引文列表中“等”和“et al”混排 for LibreOffice
](https://www.zhihu.com/question/39156067/answer/145700137)

通过本文的简单介绍，可以宏观了解 Zotero 等文献管理软件是如何控制参考文献索引与书目的格式，还能够针对不同的格式需求，提供寻找相应的解决方法的方向。希望通过本文的梳理，帮助到更多陷入使用类似软件，却不知道如何上手修改格式的朋友。欢迎更多的意见和建议。
