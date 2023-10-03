# 关于 PDF 和 Word 的那些事

## 什么是 pdf

PDF格式其实也不是什么近些年来才兴起的神秘文档格式，而是早在1990年代的时候就已经被开发出来，比起Word文档格式只晚了七年多而已。

PDF格式诞生之初的设计概念就是为了能够更好地适应不同文档格式平台之间的传播和阅读，所以相比起传统的Word、Excel、PPT、txt、Html等文档适用于日常办公和学习编辑的需要，PDF格式更倾向于以一种打印出来的电子纸张做好不同格式文档之间的跨平台交聊和传播工作。

除此之外，PDF格式还因为其兼容不同文档格式互相转码、保真性以及压缩保质等优势一经推出便坐稳了文档格式界的头把交椅。

PDF 的本质是使用**标记语言**描述了文档上面的几何结构，就像矢量图一样，所以其内容无法编辑。简单来说，PDF相当于一本书，你在阅读这本书之前，图片和文字已经定型了，可以阅读，但不能直接进行修改编辑。即使是修改，也只是在表面进行涂改，无法变动里面的内容和格式。

## 什么是 Word(doc, docx)

**doc**英文的全称是 Document，是微软自己的一种专有文件格式。 doc 格式可以容纳文字格式、脚本语言等，比 RTF、HTML 等要多，但该格式还是属于比较封闭的格式，兼容性也较低。其本身直接以**二进制**方式保存文本。

**docx**格式的文件本质上是一个 ZIP 文件。 将一个 docx 文件的后缀改为 ZIP 后是可以用解压工具打开或是解压的。事实上，Word 2007 的基本文件就是 ZIP 格式的，他可以算作是 docx 文件的容器。 docx 格式文件的主要内容是保存为 XML(扩展标记语言) 格式的，可被其它软件进行读取。

以上两种格式都是为了**编辑而生**的，十分擅长灵活修改。从这里也能看出，**PDF 和 Word 的格式在数据底层就是不同的**，Word 相当于存储的是出版物的设计文档，而 PDF 是已经印成书了。

## 二者互转

<font color="red" style="font-weight:bold;font-size:large">只有傻子才会给 PDF 转 Word 付费</font>

二者互转本来就是**难为人**，我看不起那些只会扔一个 PDF 给打工人然后默认他能像 Word 一样编辑的领导 or 老板。任何有计算机基础的人，对于自己编写的文档，都会自行保存原始格式（Word、LaTeX 等），不会只留一个 pdf 文档。

![pdf meme](https://images7.memedroid.com/images/UPLOADED109/56c9a5ba97be5.jpeg)

下面这些才是**格式互转**的神：

- [PDF Shaper](https://www.pdfshaper.com/)
- Adobe Acrobat Reader Pro
- Microsoft Office（注意，WPS Office **就是个垃圾**）

有时候，我们需要 think out of the box - 为什么要转 word？如果你只是想编辑 PDF，或是往上面打字的话，为什么不试试下面这些软件：

- [PDF XChange](https://pdf-xchange.eu/pdf-xchange-editor/index.htm)
- Adobe Acrobat Reader Pro
- Adobe Illustrator（专业平面设计软件）

不想下载软件？试试在线工具：

- [pdf.io](https://pdf.io/)
- [pdf candy](https://pdfcandy.com/cn/)
- [clever pdf](https://www.cleverpdf.com/cn)

## 附加：什么是 WPS Office、MS Office 和 Word

### WPS Office

WPS 全称字处理系统，最早由国人**独立**使用汇编语言开发，可运行在上世纪命令行电脑内的软件。是很早的（比微软的 Office 早）中文文字处理系统。目前，WPS 由金山公司运营，**已经完全背离了初心**，加入了低质量（难看）付费模板、恼人的付费格式转换等臃肿付费功能（政府定制、机构定制版除外）。包含 **Word、Excel、PPT** 三大组件。

<font color="red">WPS 能免费用，但带有大量广告和会员功能</font>，但其 Linux 版本却挺好用的。

![wps route](https://pic1.zhimg.com/v2-e4232a95a6b148a31238c6e2ecb159e2_r.jpg?source=1940ef5c)

### MS Office

或称 Microsoft Office，是微软开发的字处理系统，包含 **Word、Excel、PPT、Publisher、Access** 等大量组件。注意其中 **Word、Excel、PPT** 与 WPS Office 是重名的，尽管互相兼容，但却是不同的软件。

Microsoft Office 曾在上个世纪首次推出“所见即所得”编辑技术，对那时的 WPS 造成了降维打击。

<font color="red">Microsoft Office 是付费软件，没有免费版</font>

![ms office prod](https://itechhacks.com/wp-content/uploads/2021/05/Download-MS-Office-2013.jpg)

> 关于这二者的关系，我就抱着我的 [LaTeX](https://www.latex-project.org/) 文档准备系统，看你们争论这俩 Office 到底是谁抄谁。

### Word

相信看完了上面的部分，你已经知道什么是 Word 了。**它是一种文档格式，也是两个重名的软件**，一个来自国内的金山 WPS，一个来自微软的 Office。至于二者选择哪一个，如果你问我的话，**我只推荐 Microsoft Office（微软）**。你可以在网上找到[不用付费购买](https://otp.landian.vip/zh-cn/)的内种版本的 MS Office。