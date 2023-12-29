# 解压压缩包

*仅图片来自网络，其余内容原创*

压缩包是一种将多个文件或者文件夹打包成一个文件的方式，以便于存储和传输。它通过压缩算法将文件的大小进行压缩，从而减少存储空间和传输时间。它还可以让零散的文件变成一个整体。

<font color="red">结尾有视频，但其操作并不符合一般简洁的操作，推荐在看完此文章看不懂的情况下再去查看。</font>

## 压缩包常识

压缩包，在日常生活中出现概率为 1，是每个人都要会处理的数据格式。

尽管压缩包可以直接双击打开，但这是软件为你做的自动化操作，便于**临时查看**压缩包内的内容。如果你企图运行里面的软件，一定会报错。即便你尝试去点击“提取”或其他的按钮，也会出现各种各样的奇怪错误。

手机时代的大家，可能不知道——许多软件并不是只需要一个本体就可以运行的，它还需要不少其它的文件。这些文件可能是配置文件、动态连接库等。这些文件和软件本体一起被打包成压缩包，以便于传输。**这就像是一个外国人和一位翻译一起（压缩包）来到你的国家**，而你却把翻译关在了门外（部分提取），让那位不懂你的语言的外国人自己和你交流（没有完全解压）一样，是不可能的。

**见到压缩包，首先一定要整个解压、完整解压，而不是部分提取或直接打开**。

## 如何解压

我真的很想简化这部分的教程，但现实情况就是十分复杂的。

### 情况一：新版 Windows 右键菜单

首先，**检查右键菜单**。请对压缩包右键，如果你发现右键菜单像这个样子，请点击最下方的**显示更多选项**

![win11新版右键菜单](https://img4.xitongzhijia.net/allimg/211110/130-211110225411131.jpg)

剩余步骤和下面的一样。

### 情况二：右键菜单有 **解压到 xxx (E)** 选项

然后，在右键菜单中查找有无**解压文件**选项。如果看到了类似<strong>解压到 xxx (E)</strong>这样的选项，点击即可。<font color="red" style="font-weight: bold">不要点击「解压文件」和「解压到当前文件夹」选项</font>，前者会弹出一个窗口，选项过于复杂。后者会导致当前文件夹出现一大堆文件，打乱工作空间。

![右键解压压缩包](https://gss0.baidu.com/-Po3dSag_xI4khGko9WTAnF6hhy/zhidao/wh%3D600%2C800/sign=c1b1d25c4490f60304e5944109229f23/9e3df8dcd100baa1862219d64910b912c8fc2e54.jpg)

此时你能够在相同目录下看到一个文件夹，文件夹名字和压缩包名字相同，打开文件夹，你就能看到压缩包内的所有文件了。**这才叫“完整解压”**。

太棒啦！你刚刚完成了你人生中第一个完美的压缩包解压操作！

### 情况三：右键菜单有 **7-Zip** 选项

如果你发现右键菜单有 **7-Zip** 选项，那么恭喜你，你的电脑已经安装了压缩软件，可以直接把鼠标放在 **7-Zip** 选项上，然后在右侧弹出的子菜单内点击 **提取到 xxx** 选项，其中，xxx 就是你那个压缩包的名字。

![](https://img.xz7.com/d/file/2023/04-18/e811034dca0ca8d1dfb8664c24967b54.png)

### 情况四：右键菜单没有 **解压到 xxx (E)** 选项，也没有 **7-Zip** 选项

如果你没有发现这样的选项，说明你的电脑没有安装压缩软件，需要前往软件官网下载，这些软件不默认包括在 Windows 内。具体请看文章结尾。下载并安装完成后，跳转到情况二。

## 分卷压缩

**这是进阶知识，选修**

有时我们会看到这样的压缩包，他们是一大堆文件，这叫做**分卷压缩**，是把一个大文件拆成多个小文件的方法。

![分卷压缩](https://ts1.cn.mm.bing.net/th/id/R-C.641491d7b27ce284dfc83ccb5aef2fca?rik=BUjfnKm8f2O9tA&riu=http%3a%2f%2fwww.xitongzhijia.net%2fuploads%2fallimg%2f170223%2f76-1F223101048-water.jpg&ehk=SkJ1zONdHM8%2fazLzFp0LqmlDpMnYgfuLz8ksyd2qvRQ%3d&risl=&pid=ImgRaw&r=0)

其解压方法同上，**只需选择第一个文件，右键点击「解压到 xxx (E)」即可**。但需要注意：压缩包数量必须是齐全的，否则会解压错误。

## 软件下载

如果没有看到类似的选项，说明你的**电脑没有安装压缩软件**，请前往以下广泛使用的压缩软件官网进行下载：

- [Bandizip，中文界面，适合国人的简单压缩软件](https://www.bandisoft.com/bandizip/)
- [Win RAR，老牌强大压缩软件](https://www.win-rar.com/start.html?&L=0)
- [7-Zip，老牌经典软件，是其它部分解压软件的鼻祖](https://7-zip.org/)
- [NanaZip，基于 7-Zip 开发的压缩软件](https://github.com/M2Team/NanaZip) 此软件也可在 Windows 应用商店中下载

<img src="https://z1.ax1x.com/2023/09/30/pPqRN6J.jpg" style="width:70%;max-width:700px">

## Windows 自带压缩软件

在较新的 Windows 版本中，Windows 自带了压缩软件，可以把压缩包变得像普通文件夹一样易用。但其功能较弱，bug 满天飞，不建议使用。

## 部分视频教程

<iframe src="//player.bilibili.com/player.html?aid=385091844&bvid=BV1xZ4y1v7pU&cid=771074899&p=1&autoplay=0" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" style="height:500px"> </iframe>

<iframe src="//player.bilibili.com/player.html?aid=378563761&bvid=BV1Zf4y1u7rv&cid=423359977&p=1&autoplay=0" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" style="height:500px"> </iframe>