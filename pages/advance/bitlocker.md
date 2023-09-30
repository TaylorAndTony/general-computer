# 关于BitLocker

## 检查是否加密

下面的情况表示加密了

![bitlocker envrypted](https://pic3.zhimg.com/v2-c37c52e5be17acd3dde74a105222dc36_r.jpg)

看着这个界面，很明显就是已经像文章中说的一样，**厂商和微软偷偷的开启了设备加密功能。但是红字又清晰的告诉我加密的最后一步没有完成**（自动长传密钥）。

这个时候如果你打开磁盘管理或者把硬盘拆下来放到其他机器上，可以看到硬盘处于一个**加密了又没有完全加密**的状态。

![disk encrypted](https://pic3.zhimg.com/v2-9ca7785ecdccfd0cda44453f59f8d4b6_r.jpg)

这个时候加密的主体过程实际上已经完成了，**只要你一登录微软账户（并不一定要在设备加密的对话框，任何地方都可以），你电脑上的各个硬盘都会被Bitlocker**。

理论上来说，这个Bitlocker在加密的同时会将秘钥上传到你的微软账户里，所以即使你没有手动备份秘钥，在锁盘时也可以在微软官网找到备份的秘钥（当然微软官网能不能上的去又是另外一个问题了）。

但是即使你从来没有登录过微软账户，Bitlocker也有可能在上述123456的情况发生时误触开启锁定，由于此时并没有登录微软账户，所以生成的解密秘钥不会有在线备份，**机器就会陷入【硬盘解锁需要密钥→密钥在硬盘里→硬盘被锁定无法读取→硬盘解锁需要密钥】的死循环**。

## 关闭BitLocker

关闭Bitlocker的方式非常简单，只需要在刚才的页面上点击“关闭”即可，根据数据量和硬盘性能的不同，电脑需要花费几分钟到几小时来进行解密，**在这个过程中请务必保证电源的正常连接**。

![close bitlocker encryption](https://pic1.zhimg.com/v2-870883553576b51886449a439de488e8_r.jpg)

## 误加密了怎么办

首先明确一点，**如果你在从来没有登录微软账户的情况下被加密了，那没有任何办法能找回密钥**。同时因为Bitlocker使用的加密方法非常“高级”，想要在没有秘钥的情况下访问硬盘上的数据**几乎是不可能的**，也就是说，**数据全丢了**。这种情况基本上只能格式化磁盘重装系统（微博上有一两条淘宝大神成功修复的案例，本人对其真实性持怀疑态度）。

如果你曾经登录过微软账户，那么有很大概率能在微软官网找到密钥，方法如下：

在另一台电脑/手机上登录你的微软账户，如果不知道怎么登，试试这个[网址](https://login.live.com/)：

如果登录不上，试试挂各种游戏加速器，多刷几次，基本都能登上。

进去之后找到【设备】

在里面找到你要解锁的设备（laptop是笔记本，desktop是[台式机](https://www.smzdm.com/fenlei/taishiji/)），进去后点击管理恢复密钥

然后可能会需要邮件验证，进去之后就能找到密钥了，密钥ID与蓝屏界面上对应的就是解锁密钥，输入即可解开封印。

## 查找密钥

[Microsoft 帐户 | BitLocker 恢复密钥](https://account.microsoft.com/devices/recoverykey)

https://account.microsoft.com/devices/recoverykey

**在 Microsoft 帐户中：** 在另一台设备上打开 Web 浏览器并[登录到 Microsoft 帐户](https://account.microsoft.com/devices/recoverykey?refd=support.microsoft.com)以查找恢复密钥。 这是查找恢复密钥的最可能位置。

**提示:** 可以在任何具有 Internet 访问权限的设备（如智能手机）上登录到 Microsoft 帐户。

可以使用上面的链接，也可以转到 https://account.microsoft.com/devices/recoverykey。

它应如下所示：

![Microsoft 帐户中的 BitLocker 恢复密钥面板](https://support.content.office.net/zh-cn/media/d3ac4379-1478-41d9-870b-4cdbee24eb55.png)

BitLocker 恢复密钥忘了、找不到了，怎么办。不搞那些花里胡哨的，直接去微软官网登录账号就找到了。
网址：https://account.microsoft.com/devices/recoverykey?refd=support.microsoft.com

## 找不到bitlocker

在win11中打不开bitlocker只需要三个操作步骤即可解决，本答案通过联想电脑进行操作演示，具体操作步骤如下： 

**输入快捷命令**

win+r打开电脑运行窗口，在窗口栏中点击输入services.msc命令

**选择设置选项**

在跳转的窗口栏中，点击选择BitLockerDriveEncryptionService设置选项

**选择自动选项**

在跳转的窗口栏中，点击将模式更改为自动设置选项即可

## 后继

为了防止小白们看不懂上面的科普，这里再总结一下各种电脑Bitlocker的情况：

**如果是2019年之前买的电脑或者是组装机**，Bitlocker是默认关闭的，完全不用担心相关的问题；

**如果是2020至今买的笔记本或者品牌台式机，Bitlocker有可能是默认打开的**，机器越新默认开启的概率越大。在开启Bitlocker的机器上，又可以分为两种情况：

**如果曾经登陆过微软账户**，那么你的机器硬盘已经被加密，日常使用并不会有明显的影响（由于实时加密的缘故，CPU和硬盘的性能会受到小幅度的占用），在硬件改动或者系统发生BUG时，硬盘会被锁定，你只能花几十分钟去微软官网上找密钥来解锁，带来不必要的麻烦；

**如果从来没有登录过微软账户**，那么你的机器硬盘处于一个加密进度条99%的状态，平时与未加密的硬盘表现基本无异，然而一旦发生123456中的异常锁定情况，硬盘会被锁死而且无法找回密钥，数据丢失。这是最危险的一种情况。

为什么Bitlocker之前一直不受重视，而最近几个月却被大量电脑厂商默认开启呢？个人认为，这可能是微软的一次“试水”行为。众所周知，微软最近在大力宣传win11的安全功能，官方途径的win11需要支持TPM（一种安全模块）才能正常安装，而恰好Bitlocker也要依赖TPM。大量新电脑突然整齐划一的默认开启Bitlocker，不由得让人怀疑这是不是微软为了强推安全功能而对电脑厂商提出的新要求。**而对于绝大多数没有高等级数据加密需求的用户来说，Bitlocker有百害而无一利**，只能增加数据丢失的风险。为了你的数据安全，新电脑请到手就关闭这个功能。

截至本文完成之际，GG已经有三位同事遭遇BitLocker锁定，其中一位通过微软账户找回了密钥，另外两位选择全盘格式化数据全丢。网上也时常能看到毕业生因为硬盘被锁导致毕业设计延期崩溃的案例。再次提醒大家，**重要数据请一定做好备份！**

本文不求点赞不求打赏，只希望看到的值友能传播出去，尤其是最近新买了电脑的朋友，能救一个是一个。

## 命令行工具 manage-bde

### 将 manage-bde 与操作系统卷配合使用

下面列出了操作系统卷的基本有效命令示例。 通常，仅 `manage-bde -on <drive letter>` 使用 命令会使用仅限 TPM 的保护程序且没有恢复密钥来加密操作系统卷。 但是，许多环境需要更安全的保护程序（如密码或 PIN），并且希望能够使用恢复密钥恢复信息。 建议向操作系统卷添加至少一个主保护器和恢复保护程序。

使用 manage-bde 时的一个好做法是确定目标系统上的卷状态。 使用以下命令确定卷状态：

PowerShell复制

```powershell
manage-bde -status
```

此命令返回每个卷的目标卷、当前加密状态、加密方法和卷类型 (操作系统或数据) ：

```
可以使用 BitLocker 驱动器加密
保护的磁盘卷:
卷 D: []
[数据卷]

    大小:              1863.00 GB
    BitLocker 版本:    无
    转换状态:          完全解密
    已加密百分比:      0.0%
    加密方法:          无
    保护状态:          保护关闭
    锁定状态:          已解锁
    标识字段:          无
    自动解锁:          已禁用
    密钥保护器:        找不到

卷 C: []
[OS 卷]

    大小:              475.69 GB
    BitLocker 版本:    无
    转换状态:          完全解密
    已加密百分比:      0.0%
    加密方法:          无
    保护状态:          保护关闭
    锁定状态:          已解锁
    标识字段:          无
    密钥保护器:        找不到
```

![使用 manage-bde 检查加密状态。](.\img\manage-bde-status.png)

以下示例演示如何在没有 TPM 芯片的计算机上启用 BitLocker。 在开始加密过程之前，必须创建 BitLocker 所需的启动密钥并将其保存到 U 盘。 为操作系统卷启用 BitLocker 时，BitLocker 将需要访问 U 盘以获取加密密钥 (在此示例中，驱动器号 E 表示 U 盘) 。 系统将提示重启以完成加密过程。

PowerShell复制

```powershell
manage-bde –protectors -add C: -startupkey E:
manage-bde -on C:
```

非 TPM 硬件上的启动密钥保护程序的替代方法是使用密码和 **ADaccountorgroup** 保护程序来保护操作系统卷。 在此方案中，首先添加保护程序。 若要添加它们，请使用以下命令：

PowerShell复制

```powershell
manage-bde -protectors -add C: -pw -sid <user or group>
```

### Windows PowerShell 的 BitLocker cmdlet

Windows PowerShell cmdlet 为管理员提供了一种在处理 BitLocker 时使用的新方法。 使用 Windows PowerShell 的脚本功能，管理员可以轻松地将 BitLocker 选项集成到现有脚本中。 以下列表显示可用的 BitLocker cmdlet。

```
**Add-BitLockerKeyProtector**

    ADAccountOrGroup
    ADAccountOrGroupProtector
    “确认”
    MountPoint
    密码
    PasswordProtector
    Pin
    RecoveryKeyPath
    RecoveryKeyProtector
    RecoveryPassword
    RecoveryPasswordProtector
    服务
    StartupKeyPath
    StartupKeyProtector
    TpmAndPinAndStartupKeyProtector
    TpmAndPinProtector
    TpmAndStartupKeyProtector
    TpmProtector
    WhatIf

**Backup-BitLockerKeyProtector**

    “确认”
    KeyProtectorId
    MountPoint
    WhatIf

**Disable-BitLocker**

    “确认”
    MountPoint
    WhatIf

**Disable-BitLockerAutoUnlock**

    “确认”
    MountPoint
    WhatIf

**Enable-BitLocker**

    AdAccountOrGroup
    AdAccountOrGroupProtector
    “确认”
    EncryptionMethod
    HardwareEncryption
    密码
    PasswordProtector
    Pin
    RecoveryKeyPath
    RecoveryKeyProtector
    RecoveryPassword
    RecoveryPasswordProtector
    服务
    SkipHardwareTest
    StartupKeyPath
    StartupKeyProtector
    TpmAndPinAndStartupKeyProtector
    TpmAndPinProtector
    TpmAndStartupKeyProtector
    TpmProtector
    UsedSpaceOnly
    WhatIf

**Enable-BitLockerAutoUnlock**

    “确认”
    MountPoint
    WhatIf

**Get-BitLockerVolume**

    MountPoint

**Lock-BitLocker**

    “确认”
    ForceDismount
    MountPoint
    WhatIf

**Remove-BitLockerKeyProtector**

    “确认”
    KeyProtectorId
    MountPoint
    WhatIf

**Resume-BitLocker**

    “确认”
    MountPoint
    WhatIf

**Suspend-BitLocker**

    “确认”
    MountPoint
    RebootCount
    WhatIf

**Unlock-BitLocker**

    AdAccountOrGroup
    “确认”
    MountPoint
    密码
    RecoveryKeyPath
    RecoveryPassword
    RecoveryPassword
    WhatIf
```

与 manage-bde 类似，Windows PowerShell cmdlet 允许配置超出控制面板中提供的选项。 与 manage-bde 一样，在运行 Windows PowerShell cmdlet 之前，用户需要考虑他们正在加密的卷的特定需求。

一个很好的初始步骤是确定计算机上的卷 () 的当前状态。 可以使用 cmdlet 执行此操作 `Get-BitLockerVolume` 。

`Get-BitLockerVolume` cmdlet 输出提供有关卷类型、保护程序、保护状态和其他详细信息的信息。

### 实操

以下示例演示如何仅使用 TPM 保护程序在操作系统驱动器上启用 BitLocker：

PowerShell复制

```powershell
Enable-BitLocker C:
```

在下面的示例中，添加了一个额外的保护程序 StartupKey 保护程序，并选择跳过 BitLocker 硬件测试。 在此示例中，无需重新启动即可立即启动加密。

PowerShell复制

```powershell
Enable-BitLocker C: -StartupKeyProtector -StartupKeyPath <path> -SkipHardwareTest
```

### 关闭

方法一：

1. 以管理员身份运行**命令提示符**

2. 输入命令`manage-bde -?`（注意-？前面有空格）可以得到这个命令的各项提示；

3. 关闭bitlocker服务 `manage-bde -off C:`（注意路径前面也有一个空格）。

补充下可以用把off字段改成status查看解密进度 `manage-bde -status`


方法二：

cmd中输入以下命令关闭

```bash
manage-bde -off C:
```

但是有时候出现如下提示：

```
错误：此卷存储可以对其他卷进行自动解锁的一个或多个外部密钥。必须首先删除此类密钥，才能解锁此卷。
```

此时需要先执行如下命令：（系统分区不是C的话更改下面的盘符）

```bash
manage-bde -autounlock -ClearAllKeys c:
```

然后再执行即可

```bash
manage-bde -off C:
```

提示解密进行中，需要一定的时间
