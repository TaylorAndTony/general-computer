# edge浏览器非全屏看视频变灰

在线观看非全屏视频的时候，点击播放头两秒是正常的，紧接着就蒙上一层灰一样。然后点击其他标签页又切回来，又一个循环。

## D3D11on12

edge地址框输入`edge://flags`接着搜索`Choose ANGLE graphics backend`设置如图下 `D3D11on12`

![edge flags setting](https://img-blog.csdnimg.cn/20210717121642768.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzEwNTI1MA==,size_16,color_FFFFFF,t_70)

**注意：经过实测（2023-10-29）这个办法会导致浏览器意外崩溃**，设置为 `D3D9` 即可避免问题出现。

## 关闭增强

进入设置 - 隐私、搜索和服务 - 关掉在Edge中增强图像

## B站弹幕发白

在NGA搜到的某方法，应该同时适用于edge和chrome（毕竟内核相同）。地址栏输入 `edge://flags` 或 chrome://flags，搜索 `D3` ，出现下面这个选项。默认是Default，经逐个测试发现，只有D3D9能让弹幕恢复正常。
我平时是用50%透明度的弹幕，正常显示效果如下。

![修改为D3D9](https://img-blog.csdnimg.cn/4381cf2e94494b2783e74f6ccf6f6fca.png)

## 文字发白

若网页文本图标颜色也很暗淡灰白，edge地址框输入`edge://flags`接着搜索`Force color`设置如图下 `sRGB`

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210717121758327.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzEwNTI1MA==,size_16,color_FFFFFF,t_70)