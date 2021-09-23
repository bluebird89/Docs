## 文档

#write #tool

- 方法
  - 按人物
  - 事件
  - 概念
  - 流程
- 流程
  - 记录
  - 整理
- 概念用文档整理
- 写作系统、待办事项提醒、笔记系统
- 结构化用思维导图，不宜太详细

### 技术文档

- [ShowDoc](https://www.showdoc.com.cn/)一个非常适合IT团队的API文档、技术文档工具

## 笔记软件

- 文件夹管理 一篇笔记只能存放在一个文件夹下，限制一篇笔记被发现的几率
- 标签 顺着笔记的其他标签继续往下寻找新笔记，很难能够原路返回
- 跨平台，同时支持桌面电脑（Windows，Mac，Linux）和手机（Android，iOS）。
- 随时同步，打开任何一台机器，都能接着上一次的工作继续写。
- 实时存储，如果软件突然关闭，也不会丢失内容。
- 支持 Markdown 格式，便于后期直接发布。
- 支持推送到远程 Git 仓库，产生历史版本，同时作为远程备份。

  ### 工具

- [Paper](http://www.fiftythree.com/):优雅，美观，做笔记，记录灵感

- [语雀](https://www.yuque.com)

- [Google文档](https://docs.google.com/document/u/0/)

- [腾讯文档](https://docs.qq.com/) 对标Google docs

- [youdaonote](https://note.youdao.com/)

- [simplenote](https://app.simplenote.com/) 格式简单、跨平台同步

- Google keep

- ios notes

- OmniFocus

- [OneNote](https://products.office.com/zh-CN/onenote)

- [TickTick](https://ticktick.com/webapp)

- [石墨文档](https://shimo.im)

- [mkdocs](https://github.com/mkdocs/mkdocs):Project documentation with Markdown. <http://www.mkdocs.org>

- [joplin](https://github.com/laurent22/joplin):Joplin - an open source note taking and to-do application with synchronization capabilities for Windows, macOS, Linux, Android and iOS. Forum: [Joplin Forum - Joplin Forum](https://discourse.joplinapp.org/) [https://joplinapp.org,需要自己搭建存储](https://joplinapp.org,%E9%9C%80%E8%A6%81%E8%87%AA%E5%B7%B1%E6%90%AD%E5%BB%BA%E5%AD%98%E5%82%A8)
  - `brew cask install joplin`
  - `wget -O - https://raw.githubusercontent.com/laurent22/joplin/master/Joplin_install_and_update.sh | bash`

- [P3X OneNote](link)： a cloud-based note-taking application and is considered as an exact alternative to the well known Microsoft OneNote application

- [Roam Research](https://roamresearch.com/)

- [Simple note](https://standardnotes.org)

- [Grace Note](https://grace-note.app/#/)

- [Craft](https://www.craft.do/)

- evernote
  - [Tusk](https://github.com/klaussinani/tusk):Refined Evernote desktop app <https://klaussinani.github.io/tusk>

- [vnote](https://github.com/tamlok/vnote)A note-taking application that knows programmers and Markdown better.

- [Org Mode](https://orgmode.org/)

- [Standard Notes](https://standardnotes.org)

- [TiddlyGit](https://github.com/tiddly-gittly/TiddlyGit-Desktop)

- [telegra.ph](https://telegra.ph)

- [GoodNotes](https://www.goodnotes.com/zh-cn/)

### [Obsidian](https://obsidian.md/)

A second brain, for you, forever. [学习链接](obsidian://open?vault=Obsidian%20Help&file=Start%20here)

- 自由移动预览布局
- 图谱 对图谱中的节点所含的内容进行检索筛选
- 大纲视图对内容的组织，改观内容结构
- markdown 语法
  - 支持折叠
- backlink 内部page链接 `[[file]]`
  - 笔记 A 和笔记 B 建立链接关系
  - 作为实体链接
  - 预览模式下跨文件预览
  - 大纲引用 `[[file#heading]]`
  - 块引用 `[[file|display text]]`
  - link block [[php#^60d892]]
- 块引用 `![[obsidian]]`
  - `![[git#Git commit with gpg]]`
- 支持  LaTex math 数学公式 $E=mc^2$
- 支持 `obsidian://` 定向链接，利用超链接跳转到 Obsidian 中的特定笔记
  - 支持软件内插入 pdf [[comprehensive_python_cheatsheet.pdf]]
  - 在 pdf 语句直接添加链接，从而跳转到相对应笔记处
- 支持模板片段
  - 片段模板 放在 tempalte 文件夹下
  - insert template
- 内建的录音器甚至可以直接录音后在文件中插入音频内容
- `#` 作为 tag 使用
  - 通过 tag 打在个体身上,实体关系虚化
  - 完全打破原来层级关系
  - 原子化 打散平行
  - 通过图谱显示关系

#### theme

- California Coast
- Dracula
- Discordian

#### plugins

- Advanced Tables
	- 只需要输入「| + 作为标题的文字」，再按下 Tab，就会触发插件的自动补全语法。
	- 通过 Tab/Shift + Tab 来在表格之间移动光标，通过 Enter 完成输入
- Auto Link Title 则会在粘贴链接的时候自动抓取网页的标题，填充为文字
- Better Word Count
- Calendar
- Checklist，将不同文件的待办事项汇总到单一视图。
- Convert Url To Preview
- Day Planner
- Editor Syntax Highlight
- Kanban
- Markdown Prettifer
- Mind Map of Document
- 输入时间更自然：Natural Language Dates
- Note Refactor
	- 要为已经写过的文字创建 Wiki 链接
	- 选中一段文字，然后按下设置的快捷键，就能以这段文字为文件名创建新笔记，并在新的面板打开。如果笔记已经存在，会打开这个存在的笔记
- 所见即所得：Ozan's Image in Editor Plugin
- Outliner 能让 Obsidian 摇身变为简单方便的大纲工具。
	- 严格限制了列表的层级：一级列表后只能插入二级列表。
	- 让列表的编辑更方便：只需光标在一个列表条目，就能使用 Tab 对它进行操作，Ctrl + A 此时也不会再选中全文，而是一个小条目
	- 给列表的编辑界面添加了类似代码编辑器那样的层级样式，让它们看起来更有条理。
- Review
- Sliding Panes (Andy Matuschak Mode) ，这个插件改变了主工作区中窗格的处理方式-灵感来自于Andy Matuschak笔记中的用户界面。工作区不再缩小以适应面板，面板将保持固定的宽度并堆叠起来，它们之间会随着焦点而自动伸展
- Vantage
- Todoist
- Tracker
- 连通 ANKI 的插件
- LYT Kit

#####  Dataview 生成 MOC

- 生成 包含同样关键字|同一个标签|同一个作者书目 的目录
- list	展现形式。创建列表，还有 table、task 可以选择	必要
- from	检索范围。从哪个文件夹（写在双引号里面），或者标签（写在#后面）非必要
- where	聚合条件。contains(file.name,"Dataview") 就是匹配文件名为 “Dataview” 的文件	非必要
- sort	排序，根据什么做排序。 sort file.ctime 就是根据文件的创建时间正序	非必要

```dataview
list
from "Knowledge"
where
contains(file.tags, "computer")
sort file.ctime
```

```dataview
table autuor,from,tags
from ""
where contains(type, "book")
sort author desc
```

#### keyMap

- ctrl + ` setting
- ctrl +shift + click open in new tab

#### 技巧

- topic 这篇笔记甚至可以不存在，在写的时候写下，然后 Obsidian 会生成链接，只需要点击就可以快速的创建这个 topic

#### 主题写作

- 写作之难，在于把网状的思考，用树状的语法结构，转换成线性字符串。（"The Web, the Tree, and the String"）。

### [Sublime Text](sublime.md)

### [Notion](notion.md)

## PPT

- [remark](https://github.com/gnab/remark)A simple, in-browser, markdown-driven slideshow tool.http://remarkjs.com/
- [slideshare](https://www.slideshare.net/):Share what you know and love through presentations, infographics, documents and more
- [mdx-deck](https://github.com/jxnblk/mdx-deck):MDX-based presentation decks
- [Marp](https://marp.app/) Markdown Presentation Ecosystem
- [Slidev](https://github.com/slidevjs/slidev)
- [md2googleslides](https://github.com/gsuitedevs/md2googleslides):Generate Google Slides from markdown

## Posters

- [pics](https://github.com/corkami/pics):Posters, drawings...

## [asciidoctor](https://github.com/asciidoctor/asciidoctor)

💎 A fast, open source text processor and publishing toolchain, written in Ruby, for converting AsciiDoc content to HTML5, DocBook 5 (or 4.5) and other formats. <https://asciidoctor.org>

```sh
gem install asciidoctor

gem install asciidoctor-diagram
sudo apt-get intall openjdk-8-jre-headless  install graphviz

asciidoctor -r asciidoctor-diagram xxx.adoc
```

## 思维导图

- [FreeMind](http://freemind.sourceforge.net/wiki/index.php/Main_Page)
- xmind：结构化整理
- [MindMaster](https://www.edrawsoft.com/mindmaster/)
- [mindmeister](https://www.mindmeister.com)
- [百度脑图](https://naotu.baidu.com)
- 一起写 yiqixie.com
- [MindNode 2](https://mindnode.com/)（收费）
  - MindNode Pro
- Mindly
- iMindMap
- 参考
  - [mindtools](https://www.mindtools.com/)
  - [](https://github.com/ssjssh/notes)
  - [](https://github.com/TeamStuQ/skill-map)程序员技能图谱  github.com/teamstuq/skill-map

### 图书

- 《[思维导图完整手册-东尼·博赞](https://weread.qq.com/web/reader/5b13206071691b685b1ec84kc81322c012c81e728d9d180)》2018：东尼·博赞是思维导图的原创者，推荐首次阅读。
- 《[看完就用的思维导图-刘艳](https://weread.qq.com/web/reader/82c32870718caa2d82c928b)》2019：作者是思维导图原创者东尼·博赞所认可的，有非常详实的实践。
- 《[21天学会思维导图-尹丽芳](https://weread.qq.com/web/reader/a5532da07192ea39a55a56a)》2019：作者是文科生，手绘能力强，而且是思维导图原创者东尼·博赞所认可的。
- 《[思维导图高效记忆古诗词-张维 谢庆平](https://weread.qq.com/web/reader/a3a32c1071914618a3abcc2)》2019：思维导图适合用来记忆小学的75首诗词。
- 《[思维导图宝典：好看又好用的导图大全集-吴帝德](https://weread.qq.com/web/reader/48e323405e1ac348e1be65b)》2017：作者的话——我坚信，这应该是一本分量十足的关于思维导图的书，我以自己的亲身经历，将能设想到的大部分构思都通过案例的方式来展现给各位读者，通过文字讲述了我画每一幅思维导图的思考过程，我想，这应该是市面上相关书籍里独一无二的。

## [OmniGraffle](https://www.omnigroup.com/omnigraffle)

## [deepnote](https://deepnote.com/)

a new kind of data science notebook. Jupyter-compatible with real-time collaboration and easy deployment. Oh, and it's free

## pdf

- [paperplane](https://www.paperplane.app/):High quality HTML to PDF conversion API for developers
- [pdf2htmlEX](https://github.com/coolwanglu/pdf2htmlEX):Convert PDF to HTML without losing text or format. <http://coolwanglu.github.com/pdf2htmlEX/>

## [LaTex](https://www.latex-project.org/)

LaTeX is a high-quality typesetting system; it includes features designed for the production of technical and scientific documentation. LaTeX is the de facto standard for the communication and publication of scientific documents. LaTeX is available as free software.

- Leslie Lamport 在 TeX 基础上按内容/格式分离和模块化等思想建立的一集 TeX 上的格式。

### TeX

- 诞生于20世纪70年代末到80年代初的一款计算机排版软件，用来排版高质量的书籍论文，特别是包含有数学公式的文章书籍。
- 原始的TeX已经有了一组宏集，也就是Knuth所写的著名的Plain TeX

```sh
brew install caskroom/cask/mactex

sudo apt install texlive-latex-extra

```

### 公式

- [mathjax](https://github.com/mathjax/MathJax):A JavaScript display engine for mathematics that works in all browsers <http://www.mathjax.org/>
  - [mathjax/MathJax-docs](https://github.com/mathjax/mathjax-docs)
- [LaTeX公式编辑器](www.latexlive.com)

### 教程

- [Learn LaTeX](https://www.learnlatex.org/en/)

### 工具

- 套装
  - [TeX Live](https://www.tug.org/texlive/):国际TeX用户组织TUG开发,支持不同的操作系统
  - [MacTeX](http://www.tug.org/mactex/):使得科技文档的排版更加直观和方便
- 编辑器
  - LyX 更复杂，更专用的LaTeX编辑器，具有出色的文档 `sudo apt install lyx`
  - [TeXstudio](http://texstudio.sourceforge.net/) 开源免费的编辑器，界面整洁集成度好.功能丰富 `sudo apt install texstudio`
  - Texmaker `sudo apt install texmaker`
  - `sudo apt install gummi`
- [mathpix](https://mathpix.com):Convert images to LaTeX

## [Graphviz](http://graphviz.org/)

```sh
sudo apt install graphviz
```

## 记忆

### [anki](https://apps.ankiweb.net/)

- 特点
  - 可以插入文字、图片（拍照/截图都可以）、音频等
  - 多端同步,随时随地可以进行
  - 利于复习记忆，按照艾宾浩斯遗忘曲线，安排合理的复习频率
  - 一次记忆一个卡片上的一个小知识点，记得牢，而且能够充分利用碎片时间
- 网页版注册-》客户端登录
- 使用电脑版做笔记
- 卡片模板
  - 正反记忆
- 复习模式
- 数据统计功能

## Octave

- 安装
- 依赖
  - open-mpi
  - veclibfort
  - arpack
  - ghostscript
  - epstool
  - fftw
  - jasper
  - netpbm
  - fig2dev
  - fltk
  - gl2ps
  - glpk
  - libcerf
  - pixman
  - cairo
  - graphite2
  - harfbuzz
  - pango
  - qt
  - gnuplot
  - graphicsmagick
  - szip
  - hdf5
  - libogg
  - flac
  - libvorbis
  - libsndfile
  - portaudio
  - libde265
  - shared-mime-info
  - x265
  - libheif
  - libomp
  - ilmbase
  - openexr
  - openjpeg
  - imagemagick
  - plotutils
  - pstoedit
  - qhull
  - qrupdate
  - metis
  - suite-sparse
  - sundials and texinfo
- [wiki](https://wiki.octave.org)
- [doc](https://octave.org/doc/interpreter/)

```sh
brew install octave
```

## 工具

- [peach](https://github.com/peachdocs/peach):Peach is a web server for multi-language, real-time synchronization and searchable documentation. <https://peachdocs.org>
- [WeasyPrint](https://github.com/Kozea/WeasyPrint):WeasyPrint converts web documents (HTML with CSS, SVG, …) to PDF. <https://weasyprint.org/>
- [trix](https://github.com/basecamp/trix):A rich text editor for everyday writing <https://trix-editor.org/>
- [docute](https://github.com/leptosia/docute):📜 Effortlessly documentation done right. <https://docute.org>
- [Docusaurus](https://github.com/facebook/Docusaurus):Easy to maintain open source documentation websites. <https://docusaurus.io>
- [docxtemplater](https://github.com/open-xml-templating/docxtemplater):Generate docx and pptx (microsoft word documents) from templates, from Node.js, the Browser and the command line / Demo: <https://docxtemplater.com/demo> <https://docxtemplater.com>
- [mdx](https://github.com/mdx-js/mdx):JSX in Markdown for ambitious projects <https://mdxjs.com>
- [prezi](https://prezi.com/pricing/edu/)
- [hopscotch](https://github.com/linkedin/hopscotch):A framework to make it easy for developers to add product tours to their pages.
- [gitpitch](https://github.com/gitpitch/gitpitch):The Markdown Presentation Service For Everyone on GitHub, GitLab, Bitbucket, GitBucket, Gitea, and Gogs. <https://gitpitch.com>
- [enquirer](https://github.com/enquirer/enquirer):Stylish, intuitive and user-friendly prompt system.
- [typo.css](https://github.com/sofish/typo.css):中文网页重设与排版：一致化浏览器排版效果，构建最适合中文阅读的网页排版 <http://typo.sofi.sh>
- [unified](https://github.com/unifiedjs/unified):☔ friendly interface backed by an ecosystem of plugins built for creating and manipulating content <https://unified.js.org>
- [mkdocs](https://github.com/mkdocs/mkdocs):Project documentation with Markdown. <http://www.mkdocs.org>
- [docz](https://github.com/pedronauck/docz):✍🏻It has never been so easy to document your things! <https://docz.site>
- [Ghost](https://github.com/TryGhost/Ghost):The platform for professional publishers <https://ghost.org>
- [mailcow-dockerized](https://github.com/mailcow/mailcow-dockerized):mailcow: dockerized - 🐮 + 🐋 = 💕 <https://mailcow.email>
- [wizard](https://github.com/mylxsw/wizard):Wizard是一款开源的文档管理工具，支持Markdown/Swagger/Table类型的文档。 <http://wizard.aicode.cc>

## 参考

- [What nobody tells you about documentation](https://www.divio.com/blog/documentation/)
- [myslide](https://myslide.cn)
