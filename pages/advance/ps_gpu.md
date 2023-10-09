# 解决 Photoshop 22.3.1 和 22.4 以上版本无法检测显卡的方法

就是从22.3.1版本开始，Photoshop引入了新的gpu检测机制，但是22.3.1引入新机制后引发了一个严重的bug：绝大多数显卡都无法被检测(无论是老显卡还是新显卡)。当时adobe社区就炸了，一堆人在发帖询问。

直到前阵子Photoshop发布了22.4，官方的说法是22.4修复了这个bug，如果你的电脑依旧无法检测出来显卡，那么你电脑的显卡就是被Photoshop放弃的显卡，意思就是Photoshop不再支持你的显卡了，你的显卡太老了。

## 方案 1：强制开启 GPU

别急，Adobe没有把事做绝，留了一个强制使用旧版gpu的方法，但是由此引发的一系列不稳定性问题，用户自己负责：

Windows: `[系统磁盘]:\Users\[用户名]\AppData\Roaming\Adobe\[Photoshop_版本号]\[Photoshop_版本号]Settings\`

macOS: `//Users/[用户名]/Library/Preferences/[Photoshop_版本号]Settings/`

在以上对应的目录下创建一个名为`PSUserConfig.txt`的文本文件，然后在该文本文件中填入以下内容：

```ini
# Force GPU On
GPUForce 1
```

保存，重启ps，就能检测到显卡了。

> 对于仍受支持 GPU 检测不到的情况，Adobe 官网提供了[一个方案](https://helpx.adobe.com/cn/photoshop/kb/troubleshoot-gpu-graphics-card.html)：我们遇到一个已知问题，对话框可能报告“您的图形处理器不兼容。”如果您在基于 Intel 的系统上运行 Windows 且安装有“Microsoft OpenCL/OpenGL 兼容性包”，则解决方案是卸载兼容性包并重新启动计算机。

## 方案 2：Program 文件夹

*注意：此情况可能是个例。*

在D盘根目录下出现了一个名字为`program`没有扩展名的空文件，将其删除掉问题就解决了。

我的PS安装在`D:\Program Files (x86)\Adobe\Adobe Photoshop CS6 (64 Bit)`，暂存盘设置在E盘。使用了大半年一直没有出过问题。

今天又出现了同样的问题，一看program空文件又出现了，删除之后PS正常。这个空文件似乎是我这两天玩战争雷霆才出现的。

后面我自己在D盘根目录下新建了名字为program的空文件，重启PS，PS就检测不到显卡；删除program空文件，重启PS，PS立马变正常。

用别的名字的空文件完全没有影响。

## 方案 3：卸载 PS 并清空配置

别重装系统，甚至在显卡升级到最新版本之后都没必要重装驱动。

我的做法：

1. 备份好笔刷、预设啥的你舍不得丢掉的东西

2. 卸载检测不出来的这个版本

3. 打开C:\Users\用户名\AppData\Roaming\Adobe

4. 删除对应版本的文件夹

5. 重装PS

亲测有效！

虽然是16年的问题了，但介于我也遇到了同样的困难，正好也解决了，就过来回答一下了.


## 关于独立显卡

Win 11 似乎有一些神奇的特性，导致在显卡驱动内设置 Ps 使用独立显卡，会被 Win 11 忽略，仍然运行在集成显卡上。在 Win 11 设置内分配独立显卡后，依然无法启用。即：**某些情况下，Win 11 自己认为此软件不需要独立 GPU，你就没有办法让它使用独立 GPU，此项无法修改**。若仍然希望独显运行，只能设置让整个显示输出都工作在独立 GPU 上。如果是 N 卡，临时解决方案是：前往 GeForce Experience 查看你的软件在不在列表内，用 GeForce Experience 启动你的软件即可调用独立 GPU。