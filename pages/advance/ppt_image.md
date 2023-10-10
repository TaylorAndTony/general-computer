# PPT如何导出高分辨率图片

*文章来自知乎*

关掉所有 office 的软件，在开始上点右键，点运行，输入 regedit，点击确定，就打开了注册表编辑器。

找到

```
HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\PowerPoint\Options
```

其中不同 PowerPoint 版本选择不同，2007是12，2010是14，2013是15，2016是16

我是 PowerPoint2016，所以我点的是16.0

点击`options`，点`编辑 - 新建 -DWORD(32位)值(D)` - 命名为 `ExportBitmapResolution`

（看了很多教程，按理应该电脑是32位的选32位，64位选63位的，但是我电脑是64位，然而选了64没用，反而32位是好使的，所以如果你也遇到这种问题，就选32位的试试）

点击新建好的“`ExportBitmapResolution`”，点击右键，再点击修改，先选择十进制，数值数据输入“300”，之后在注册表编辑器里选择文件 - 退出就可以了

（据说 PPT 能导出的最大分辨率是 307 dpi，然而我试了一下，貌似 700 多都可以，emmmm，难道我的 PPT 变异了？？？不过 300 dpi 够用了，太大的话照片会有好几兆，没必要这么多）

之后从 PPT 导出图片就可以了。

选择文件 - 另存为 - 保存类型可以选 JPG，PNG，科研的话可以选 tif

```python
import winreg

def hack_ppt(dpi=300, ppt_ver='16.0') -> bool:
    reg_dir = r'Software\Microsoft\Office\$\PowerPoint\Options'.replace(
        '$', ppt_ver)
    print('\n[*] Hacking PPT:', reg_dir)
    reg = winreg.ConnectRegistry(None, winreg.HKEY_CURRENT_USER)
    try:
        keys = winreg.OpenKey(
            reg,
            reg_dir,
            0,
            winreg.KEY_ALL_ACCESS)
    except Exception:
        print(f'[x] PPT version {ppt_ver} not found!')
        return False
    try:
        winreg.QueryValueEx(keys, 'ExportBitmapResolution')
    except FileNotFoundError:
        print(f"[x] PPT version {ppt_ver} Already hacked!")
        return False

    winreg.CreateKey(keys, 'ExportBitmapResolution')
    winreg.SetValueEx(keys, 'ExportBitmapResolution', 0, winreg.REG_DWORD, dpi)
    winreg.FlushKey(keys)
    winreg.CloseKey(keys)
    reg.Close()
    print(f"[v] PPT version {ppt_ver} success!")
    return True
```

