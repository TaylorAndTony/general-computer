# 给 Powershell 配置 Oh My Posh

## 去官网安装 Oh My Posh

[https://ohmyposh.dev/docs/installation/windows](https://ohmyposh.dev/docs/installation/windows)

```powershell
winget install JanDeDobbeleer.OhMyPosh -s winget
```

建议挂代理

## Nerd 字体

在电脑上安装任意一种 Nerd 字体，推荐 Fira Code Nerd Font。Nerd 通过在字体中添加特殊字符来实现图标的显示，安装 Nerd 字体可以支持 oh my posh 花里胡哨的提示符。

然后终端配置为使用 Nerd 字体。

## 配置文件

通过这个打开配置文件

```powershell
notepad $PROFILE
```

修改为

```powershell
# oh my posh
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH/bubblesline.omp.json"  | Invoke-Expression
```
固定的，`--config "$env:POSH_THEMES_PATH/bubblesline.omp.json"` 里面可以设置主题。详见[官网](https://ohmyposh.dev/docs/installation/customize)

## 启用历史记录补全

配置文件中继续加入

```powershell
# PSReadLine
Import-Module PSReadLine
# Enable Prediction History
Set-PSReadLineOption -PredictionSource History
# Advanced Autocompletion for arrow keys
Set-PSReadlineKeyHandler -Key UpArrow -Function HistorySearchBackward
Set-PSReadlineKeyHandler -Key DownArrow -Function HistorySearchForward
```

## 加速启动

如果不加 `--config "$env:POSH_THEMES_PATH/bubblesline.omp.json"` 那么 oh my posh 会在每次启动的时候去 github 上下载一个配置文件，这样会导致启动很慢。故必填 --config。