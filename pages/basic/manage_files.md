# 如何整理电脑上的文件

*除图片外，文章由本人创作*
## 引言

没有人希望自己的桌面是这样的：

![messy desktop](https://pic4.zhimg.com/v2-5449bd9bc2b8976ef559caad3b3fe2fb_r.jpg)

随着时间的推移，我们的电脑或者手机里面的文件数量会越来越多，你会越来越搞不清楚，哪些文件是需要清理的，哪些文件是需要保存的。有可能你把一个文件误删之后，在某一天你需要它的时候，却百寻不获。

## 前置知识

你可以在**资源管理器**上面看到这样的目录：

![path](https://z1.ax1x.com/2023/09/30/pPqc2Xn.png)

**目录**就是一串字符，用来指示一个文件、文件夹在何地方。在 Windows 上，它以反斜线`\\`分割每个文件夹。
例如，a 文件夹下有一个 b 文件夹，下面有一个 word.docx 文件，那么路径可以写成：

`a\\b\\word.docx`

为了方便，下文将使用 Linux 路径表示方法，以正向斜杠`/`分割路径。

<font color="deeppink" style="font-weight:bold">以下所有方法都是我自己总结的，具备实际价值。</font>

## 建立「总+分」的分类体系

在你熟悉的地方（如 D 盘内）建立一个总的文件夹，例如叫`AllMyFiles`，这个文件夹将存放你的所有**按专题分类**的文件。

### 案例 1

张三是大学生，他把学习要用的资料，都放在一个`Study`文件夹，一切文档、信息、视频全都在这里面。

在这个文件夹内，继续按照专题建立子文件夹。张三要准备四级考试，他建立了一个`CET4`文件夹，准考证、下载的资料等全都堆在这里。这里面的文件不会达到几十个，找起来非常快。

### 案例 2

李四是一个软件工程师，他平时不仅自己写软件，也喜欢搜集各大破解软件。他建立了一个文件夹叫做`Software`，他所有的软件都在这里。

在`Software`下，他又建立了`Dev`文件夹，用来存放自己写的软件。在`Dev`内，他又按照编程语言建立了不同的文件夹，在这些文件夹下，又按照每个项目建立了不同的文件夹。

最终，他的一个软件目录为`Software/Dev/Python/AutoFillTemperature`。这样，他使用不同编程语言时，也能灵活管理文件。

然后，他使用`Download`文件夹存放下载的软件。最后他的目录类似：

- 自己写的自动化工具：`Software/Dev/Python/Auto`
- 自己写的计算器：`Software/Dev/CSharp/SuperCalc`
- 网上找的破解版 Office：`Software/Download/Office_Crack`

## 有时，我只要快速定位

尽管上面的分类体系已经足够清晰，但有时我们无法避免需要立刻找到一个文件——我们记得那个文件名，但不想一次次点击文件夹进入那个地方。

**Listary**，一个仅需在任何地方键入**名字中文拼音首字母**即可全盘搜索的小工具。Listary 是一个革命性的Windows搜索工具，借助 Listary软件，你可以快速搜索电脑文件、定位文件、执行智能命令、记录访问历史、快速切换目录、收藏常用项目等。

![listary UI](https://www.listary.com/wp-content/uploads/find-as-you-type-explorer-1.png)

![listary UI](https://www.listary.com/wp-content/uploads/launch-apps3.png)

非常推荐读者前往其[官网](https://www.listary.com/)下载体验。安装后，Listary 自带一个快速上手教程。

## 忘东西，是很常见的

如果你忘记了某一个文件，或只记得他是一个包含某关键字的 word 文档，那么**Everything**全盘搜索软件就是你需要的工具。它是一个速度极快的全盘搜索工具，支持正则表达式。

![everything](https://www.voidtools.com/zh-cn/support/everything/Everything.Search.Window.png)

仅需输入文件名即可开始搜索。如果你想搜包含“说明”且以 pdf 结尾的文件，可以使用通配符：`*说明*.pdf`

若使用正则表达式，仅需用`.+` 替换 `*` 即可。上述搜索变为`.+说明.+.pdf`

> 对于懂正则表达式的读者，可能注意到了上述正则结尾的 `.pdf` 其实会额外匹配位于 pdf 前的一个任意字符，不过作为扩展名开始的小数点 `.` 依然会被匹配，故此处可以不把 `.` 转义为 `\.`

软件可以来[这里](https://www.voidtools.com/zh-cn/)下载。

欲学习正则表达式，可看[知乎](https://zhuanlan.zhihu.com/p/107294963)的这篇文章，或前往其对应的[Github仓库](https://github.com/ziishaned/learn-regex)学习。

## 开始备份

**请永远不要把重要数据只存放一份**。了解 **321 原则**：3 份文件备份，存在 2 种介质上，并做 1 份异地备份。

前面使用一个根目录来存放所有文件的好处在于，备份时，只需要备份这一个文件夹即可。备份可以选择 U 盘、移动硬盘、移动固态硬盘、NAS 等进行。

推荐使用自动化备份工具进行文件同步。例如，使用 [Robocopy](https://www.bilibili.com/read/cv19040042) 命令行工具，或 [Free File Sync](https://freefilesync.org/) 工具完成。文件同步与备份是一个很庞大的话题，此处不展开说明。