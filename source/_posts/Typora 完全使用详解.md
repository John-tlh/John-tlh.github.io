---
title: Typora 完全使用详解
categories: 
- 编程开发
tags: 
- 编辑器
- 高效工作
comments: true
---



![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4uc3NwYWkuY29tLzIwMTkvMDUvMjQvMmNiOTc1NWU2ZGUzYjg2MGVkZTBhYzA0OTUxZWYxNDcucG5n?x-oss-process=image/format,png)

# Typora 完全使用详解

@[toc]
Typora 一直是我认为桌面端笔记应用应有的终极形态。【它的功能之强大、设计之冷静、体验之美妙、理念之先进值得所有笔记应用厂商学习。】

但是一件很尴尬的事情是，由于它极简的设计理念，有许多使用者并没能完全地了解到Typora 的全部强大功能。我想在这篇文章中由浅入深地介绍Typora 的功能亮点。无论新手还是老手，相信你都能在这篇文章中发现惊喜。

<!-- more -->

## Typora 是什么？

Typora 是一款支持实时预览的Markdown 文本编辑器。它有OS X、 Windows、Linux 三个平台的版本，并且由于仍在测试中，是完全免费的。

## 一个Markdown 文本编辑器

Typora 首先是一个Markdown 文本编辑器，它支持且仅支持Markdown 语法的文本编辑。 在Typora 官网上将他们描述为 【A truly minimal markdown editor.】。

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4uc3NwYWkuY29tLzIwMTkvMDUvMjQvNDljNGNkZWY0N2JmODEwMThiOTg3MWE2Mjg1MjMwNjQucG5n?x-oss-process=image/format,png)

### 关于Markdown 

Markdown 是用来编写结构化文档的一种纯文本格式，它使我们在双手不离开键盘的情况下，可以对文本进行一定程度的格式排版。

你可以在这篇文章中[快速入手Markdown。 ](https://sspai.com/post/36610)

由于目前还没有一个权威机构对Markdown 的语法进行规范，各应用厂商制作时遵循的Markdown 语法也是不尽相同的。 其中比较受到认可的是[GFM标准，](https://github.github.com/gfm/)它是由著名全球最大同性交友网站[GitHub](https://github.com/) 所制定的。Typora 主要使用的也是GFM 标准。同时，你还可以在 `文件-偏好设置-Markdown 语法偏好 - 严格模式` 中将标准设置为【更严格的遵循GFM标准】。具体内容你可以在[官方文档](http://support.typora.io/Strict-Mode/)中查看。

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-UZYuwtpY-1582722830655)(C:\Users\xxh\AppData\Roaming\Typora\typora-user-images\image-20200226153039219.png)]

### 写得舒服

一个文本编辑器，写得舒服是关键。一个优秀的笔记应用应该给用户选择Markdown 语法风格的权力。 通过打开 `文件 - 偏好设置` 你会发现Typora 为编辑体验得考虑细致到了极点。Typora 中提供了大量有关Markdown 偏好的设置，据此，你可以构建一个几乎完全适合自己得Markdown 编辑器。下面介绍一些与文本编辑体验有关的功能亮点。

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-0dztuL2C-1582722830657)(C:\Users\xxh\AppData\Roaming\Typora\typora-user-images\image-20200226153641605.png)]

### 智能标点

我认为 【智能标点】是比较有趣的一点。它可以自动帮你将不是很美观的直引号转化为更美观的弯引号。

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-XT6JyFXv-1582722830658)(C:\Users\xxh\AppData\Roaming\Typora\typora-user-images\image-20200226154430953.png)]

### 图片插入

Typora 的图片插入功能是广受好评的。毕竟Markdown 原生不太注重图片插入的功能，但你可以在 Typora中：

- 直接使用`右键 - 复制 - ctrl + v` 将网络图片、剪贴板图片复制到文档中。
- 拖动本地图片到文档中。

Typora 会自动将你插入符合Markdown 语法的图片语句，并给它加上标题

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-O1rOdmt5-1582722830659)(C:\Users\xxh\AppData\Roaming\Typora\typora-user-images\image-20200226155053765.png)]

更强大的是，Typora 支持在拖动或 `CTRL + v` 网络图片后自动将其保存到本地。你可以在 `文件 - 偏好设置 - 图片插入` 中选择复制到哪个路径，什么情况下需要复制。

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-f8yuigwO-1582722830661)(C:\Users\xxh\AppData\Roaming\Typora\typora-user-images\image-20200226155357777.png)]

这一功能保证了即使网络源失效了，你还有本地的备份文件可用。同时也能使你的文档文件夹更合理、完整。

### 打字机模式和专注模式

- 打字机模式【使得你所编辑的那一行始终处于屏幕中央】。
- 专注模式 【使得你正在编辑的那一行保留颜色，而其它行的字体呈灰色】。

你可以在 `视图 - 专注模式 / 打字机模式` 中勾选使用这个选项。

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-xMhaTbPl-1582722830662)(C:\Users\xxh\AppData\Roaming\Typora\typora-user-images\image-20200226160003599.png)]

### 实时预览

 目前来看：到现在还不支持编辑界面实时预览的Markdown 编辑器基本就可以退出市场了。Typora 在这一方面显然已经领先了一大截——他们连Markdown 语法的标记都在实时预览中消去了。当你离开正在编辑的有格式的文本段后，Typora 会自动隐藏Markdown 标记，只留下【**所见即所得的**】美妙。他们把这称为 *Hybrid View*。![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4uc3NwYWkuY29tLzIwMTkvMDUvMjQvZjk5YzljZTAyZTI3MjhlYzZjNjRiNDQzOTQ3ZmM2N2UuZ2lm)

为了防止一些bug 的发生导致格式问题无法修改，Typora保留一个**【源代码格式】**。你可以通过 `视图 - 源代码模式` 或左下角的`</>` 按钮进入。

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4uc3NwYWkuY29tLzIwMTkvMDUvMjQvYmNkYTljNGUzNTcyNWI3Mjk3YTZiOTBkODc0NTU2NGUuZ2lm)

### 大纲/文件侧边栏

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-0noFiiFN-1582722830667)(C:\Users\xxh\AppData\Roaming\Typora\typora-user-images\image-20200226161955327.png)]

Typora 会根据Markdown 标记的H1、H2、H3······各级标题为你呈现一个大纲。

你一可以选择查看文件夹中的文件，目前Typora 只支持查看md / txt / 等多种格式的文件，还是很不错的。

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-nz9ILbwb-1582722830667)(C:\Users\xxh\AppData\Roaming\Typora\typora-user-images\image-20200226162325505.png)]

### 空格与换行换段

Typora 在空格与换行部分主要是使用Common Mark 作为标注规范。与前文提到的GFM一样，Common Mark 也是比较流行的Markdown 语言规范（解析器）之一。

- **空格：**在输入连续的空格后，Typora 会在编辑器中替你保存这些空格，但当你打印或导出时，这些空格会被省略成一个。

  你可以在源代码模式下，为每个空格前加一个 `\` 转义符，或者直接使用HTML 风格的 `&nbps；` 来保持连续的空格。

- **软换行：**需要说明的是，在Markdown 语法中，换行（line break）与换段是不同的。且换行分为软换行和硬换行。在Typora 中，你可以通过 `shift + enter` 完成一次软换行。软换行只在编辑界面可见，当文档被导出时将被保留，且没有换段的段后距。

- **硬换行：**你可以通过 `space + shift + enter` 完成一次硬换行，而这也是许多Markdown 编辑器所原生支持的。硬换行在文档被导出时将被保留，且没有换段后的段后距。
- **换段：**你可以通过 `enter`完成一次换段。Typora 会自动帮你完成两次 shift + enter 的软换行，从而完成一次换段。这也意味着在Markdown 语法下，换段是通过在段与段之间加入空行来实现的。

下附以上各空格、换行、换段、的测试结果图。具体内容可以在[官网文档中](http://support.typora.io/Line-Break/)查阅。![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4uc3NwYWkuY29tLzIwMTkvMDUvMjQvNWMyZmJhYTUzYjI3NjY2YTdmZDBiMDdhYzNlMTAwYmYucG5n?x-oss-process=image/format,png)

### emoji 表情

如今emoji 表情越来越多地出现在一些网站文章中。但在桌面端（特别是Windows系统）文本编辑器上插入emoji 是一件十分麻烦的事情。

在Typora 中，你可以用 `：emoji`的形式来打出emoji，软件会自动给出图形的提示，还是非常好用的。

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-UA57XnLd-1582722830671)(C:\Users\xxh\AppData\Roaming\Typora\typora-user-images\image-20200226165354666.png)] 

## 一个学术文档编辑器

除了基本的文本编辑体验极佳之外，Typora 还是一个非常优秀的学术文档编辑器。当然作为一个轻量级的、基于Markdown 的编辑器，它不能与那些`La Tex` 编辑器相提并论，但它仍支持了许多可用于学术写作的功能。

### `LaTeX`

> `LaTeX` 是一种基于 TEX 的排版系统，由于它易于快速生成复杂表格和数学公式，非常适用于生成高印刷质量的科技和数学类文档。如果你常阅读数学、计算机等领域的学术论文，你一定对`LaTeX` 不陌生。

Typora 原生支持 `LaTeX` 语法，你有两种方式输入 `LaTeX` 风格的数学公式：

1. **行内公式（inline）：**用`$...$`括起公式，公式会出现在行内。
2. **块间公式（display）：**用`$$...$$`括起公式（z注意`$$`后需要换行）

具体的`LaTeX` 语法在此不赘述了，可以在[这篇文章](https://blog.csdn.net/happyday_d/article/details/83715440)查看。

### 代码高亮

Typora 中代码的插入也可以分为行内和块间两种：

1. 行内代码：用`...`或``...``括起代码，代码会以主题中设置的样式出现在行内，但不会实现代码高亮。

2. 代码块：输入```后输入语言名，换行，开始写代码，Typora 就会自动帮你实现代码高亮。Typora 原生支持许多编程语言代码块的语法高亮，基本日常常用的编程语言他都能很好的支持。

   除此之外，你也可以直接换行开始写，而后再选择语言。

```php+HTML
echo "php is the best language for the web programing.";
```

### 表格

再Markdown 中插入表格一直是一件比较头疼的事情。在一般的Markdown 编辑器中，你可以通过以下的格式插入表格：

你只需要在行内 `段落 - 插入 - 表格`，并输入行数和列数，Typora 就会自动生成一张样式不错的空表格。 

|      |      |      |
| ---- | ---- | ---- |
|      |      |      |
|      |      |      |
|      |      |      |

### 链接引用与脚注

**链接引用**类似于我们常在论文末尾看到的【参考文献】的写法，你可以通过`[]:`的语法来为你的文档加上链接或引用。

**脚注**即某段结尾右上角标有数字标记，页面底部进行注释的写法。你可以在需要插入脚注标号的位置写[^1] 

[ ^1 ]:http://www.baidu.com

`再在下方通过[^ nbumber ]:`在文档中插入脚注。注意不要遗漏了脚注编号 `number`前后的空格。

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-lnvrozN3-1582722830673)(C:\Users\xxh\AppData\Roaming\Typora\typora-user-images\image-20200226173522078.png)]

### 文件系统

除了前文提到的文件侧边栏，Typora 还提供了一些耦合度不高的文件系统。

- **快速打开：**你可以通过 `文件 - 快速打开 -` 或 `CTRL + P` 快捷健快速打开最近的文档。
- **保存：**Typora 支持自动保存，一般很少有写好的文档丢失的情况。同时他也提供了诸如 【保存】、【另存为】、【保存全部打开的文件】之类的功能。
- **导入：**Typora 原生支持非常多的文件格式：`.doc/ .latex/ .tex/ .ltx/ .rest/ .org/ .wiki/ .dokuwiki/ .textile/ .opml/ .epub` 等。![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4uc3NwYWkuY29tLzIwMTkvMDUvMjQvYmEyOTVmMjFmMGI3MTY0NmJiMzZhMDUxN2U4NjhjZWQucG5n?x-oss-process=image/format,png)

## 一个伪装成文本编辑器的浏览器

事实上，如果你有一定的计算机基础，你可以找到许多有关于 【Typora 其实是一个浏览器】的蛛丝马迹。



[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-o07iC4Lo-1582722830675)(C:\Users\xxh\AppData\Roaming\Typora\typora-user-images\image-20200226174436904.png)]

在图片插入中，Typora 用了【复制图片到./${filename}.assets 文件夹】的说法，而这其实是网页前端常用的 Java script 字符串模板语法的风格。

再比如，Typora 将更遵循 GFM 标准的Markdown 语法模式称为 【严格模式 Strick Mode】，这一说法常见于HTML 和Java Script 编程中。类似【源代码模式】的说法也是同理。

当然，最明显的一点是当你按下 `shift + f12` 快捷键时，页面会弹出一个基于Chrome 的开发者工具栏，也就是我们在浏览器中常说的【审查元素】。

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-oNwL53x2-1582722830676)(C:\Users\xxh\AppData\Roaming\Typora\typora-user-images\image-20200226202721006.png)]

### 伪装从何而来？

当我们把视角放在【Typora 是一个支持Markdown 语言的文本编辑器】的出发点来考虑这个问题，一切就都明白了。

John Gruber 在2004 年用Perl 创造了Markdown 语言，这个语言的目的是希望大家使用【易于阅读、易于撰写的纯文本格式，并选择性的转换成有效的XHTML 或是 HTML】。也就是说，**Markdown 诞生之初，它就是为了被浏览器阅读而设计的。**

我们在用 Markdown 语言撰写文稿的时候，其实本质上是在借助某种编程语言的转化解析器来编写一个HTML网页。Markdown 从它诞生之初就与Web技术有着极其紧密的联系。

如果我说，我们每一篇文稿都是一个网页，那就很好理解了。Typora 利用解析器先将我们写的Markdown 文档解析成为HTML 文档，再把它嵌入一个CSS样式，最后再加上可能需要的脚本等。

### HTML

HTML 是一种标记语言，主要负责构成网页的骨架，它包含所有不加装饰的网页元素。在Typora 的使用场景下则是所有的`文本、段落、标题`等记号。

你可以把一张网页想象成一幅数字油画，HTML就是那个黑白线条的底，上面写满了数字标记，示意你哪一块区域要上什么颜色。而CSS 则负责在对应的区域涂上颜色，甚至加上一些装饰等。



![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4uc3NwYWkuY29tLzIwMTkvMDUvMjQvN2NlM2Q5ZWQyNDVlZWQ5MDJlODMzNDA1Yjk0NjQxMDMuanBn?x-oss-process=image/format,png)

#### HTML标签

Typora 支持许多常用的标签，如果你了解HTML 语法的话，你可以写出十分美观丰富的文档页面。

<span style= ‘color: red'>This is red !</span>

事实上你可以在 Typora 中完成许多基本的HTML 风格的文本输入，例如HTML 字符、HTML块、HTML 风格的注释，甚至是视频和音频。具体支持的功能和限制请在[官方文档中](http://support.typora.io/HTML/)查阅。

有了这一功能，我们就可以在Typora 中创造许多远超普通 Markdown 文档的页面效果。

#### 导出为HTML

Typora 原生文档支持将文档导出为HTML 格式的文件，并选择是否要嵌入css样式表。

除此之外，由于其本身【浏览器】的属性，你可以直接在实时预览界面用`CTRL + c`复制到HTML 代码。一个使用的用处是将这些HTML 代码直接`CTRL + v`粘贴到微信公众号后台，基本可以保证两边显示效果相同。这一点不仅使公众号推送可以有更自由、美观的样式，也让编辑、排版更轻松了。（由于微信自带浏览器的一些特征，可能有少部分CSS Style 不能生效。建议多多校对）

 ![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4uc3NwYWkuY29tLzIwMTkvMDUvMjQvM2Q4MThjMTg5MzQ2MzJiMDQzZmNmNGFkOWJlMWQwNDYucG5n?x-oss-process=image/format,png)

具体如何用Typora 完成公众号写作，你可以在`这篇文章`进一步了解。

#### CSS

为了让文档更美观，我们可以为其加上CSS Style。我认为Typora 对CSS 的支持让它成为一众桌面应用中最与众不同的一个。在Typora 中CSS 被称为【主题】，但其本质仍然是CSS 文件。你可以在 `文件 - 偏好设置 - 主题 - 打开主题文件夹` 看到这些CSS 文件。

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-9if2hpyI-1582722830682)(C:\Users\xxh\AppData\Roaming\Typora\typora-user-images\image-20200226210035252.png)]

选择不同的主题可以使文档拥有不同的外观，但不会影响内容。Typora 自带了若干主题，你也可以在[官网](http://theme.typora.io/)下载更多的主题。

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4uc3NwYWkuY29tLzIwMTkvMDUvMjQvZWZjZjY1YmE5OTNjNGJiMGIwNThkNmViODI1OGRmNmYucG5n?x-oss-process=image/format,png)

除此以外，如果你有一定的web编程基础，你当然也可以自己修改、新建适合你使用需求的CSS 文件。比如自己写一份为WeChat 的CSS 文件，来符合我公众号特定的排版需求，例如正文是15px，页边距是8，小标题是18px等等。

使用Typora 的主题功能写公众号的一个好处是，只需要每次都套用同样的主题，我们就可以在保证每次排版规范都相同的同时，节省许多重复的工作。

## 参考

1. [Front-matter -Hexo](https://hexo.io/zh-cn/docs/front-matter)
2. [让 Markdown 写作更简单，免费极简编辑器：Typora](https://sspai.com/post/30292)
3. [使用 Typora 一次性搞定公众号写作与排版](https://sspai.com/post/40524)
4. [简中求效：Markdown 遇上 LaTeX](https://sspai.com/post/36420)
5. [关于Typora + pandoc导出文件功能的介绍](https://blog.csdn.net/jiajikang_jjk/article/details/80380133)
6. [我的 LaTeX 入门](https://blog.csdn.net/shujuelin/article/details/79340373)
7. [选择正确的 Markdown Parser](https://www.cnblogs.com/lfk-dsk/p/5205969.html)
8. [Typora —— 能用 ⌘C⌘V 插图的 Markdown 编辑器](https://sspai.com/post/43301)
9. [HTML Support in Typora - Typora](http://support.typora.io/HTML/)
10. [Markdown - Wikipedia](https://zh.wikipedia.org/wiki/Markdown)
11. [Windows、Unix、Mac不同操作系统的换行问题-剖析回车符\r和换行符\n](https://blog.csdn.net/tskyfree/article/details/8121951)
12. [简中求效：Markdown 遇上 LaTeX](https://sspai.com/post/36420)
13. [通用标注 (CommonMark)](http://www.commonmark.cn/w/)
14. [Whitespace and Line Breaks - Typora](http://support.typora.io/Line-Break/)

## ENDING

------



dn.net/tskyfree/article/details/8121951)
12. [简中求效：Markdown 遇上 LaTeX](https://sspai.com/post/36420)
13. [通用标注 (CommonMark)](http://www.commonmark.cn/w/)
14. [Whitespace and Line Breaks - Typora](http://support.typora.io/Line-Break/)

## ENDING

------



