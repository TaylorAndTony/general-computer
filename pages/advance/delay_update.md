# 无限期推迟 Windows 自动更新

*文章来自网络*

## 暂停更新3000天

```bash
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings" /v FlightSettingsMaxPauseDays /t reg_dword /d 3000 /f
```

## 去掉信息流

```bash
reg add "HKEY_CURRENT_USER\SOFTWARE\Policies\Microsoft\Windows\explorer" /v DisableSearchBoxSuggestions /t reg_dword /d 1 /f
```

## 搜索栏热点

win11专业版或企业版最新版关闭"搜索栏热点"的具体方法：设置->隐私和安全->搜索权限->更多设置->显示搜索要点，关闭该选项即可关掉所有搜索栏中的热点信息。