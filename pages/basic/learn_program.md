# 普通人要不要学编程

*全文原创*

下文将“学习编程语言”理解为学习主流的计算机编程语言，如 Python、Java、C/C++、C# 等，而不是抖音、快手上所谓的“黑客”用来闪屏的小技巧。

先说答案：**你可以用一个简单的方法，判断自己要不要接触编程语言——“我平时如何使用电脑？”**

## 前置知识

**编程语言**可以简单的理解为一种计算机和人都能识别的语言，它他看起来就像电影里黑客的电脑上闪烁的符号（尽管我十分反对这种类比），且现在各类编程语言的入门课程十分火爆，即使你没有需求也给创造需求，辅导班大肆推销自己的课程，贩卖焦虑，宣传自己的课程有多好……

编程语言可以分为不同的类型，如高级语言和低级语言。高级语言更加接近自然语言，使用起来更加方便，例如 Python、Java 和 C++ 等。低级语言更加接近计算机底层的二进制代码，例如汇编语言。

使用编程语言，我们可以编写各种各样的程序，从简单的计算器到复杂的应用程序和游戏。编程语言提供了一系列的命令和指令，通过组合这些命令和指令，我们可以完成各种任务，比如数据处理、逻辑判断、循环控制等。

编程语言一直充满活力——我们听说过的编程语言，许多都源自上个世纪。而 2010 年附近出现了如 Golang、TypeScript、Rust 等新兴编程语言。同时还有如 Erlang、Elixir、Nim、Haskell、F# 等小众编程语言。


## 从使用习惯出发

**对于普通人来说，编程语言最大的作用就是“自动化”**

### 没必要学习的情况

如果除开工作、学习、娱乐，电脑对你来说是可有可无的——电脑唯一的作用便是偶尔写文档和表格，当有人发来文档时，我就打开电脑，编辑完，就不再用了。那么，**不建议学**。编程语言的主力战场是电脑、笔记本，而不是手机。

如果你是狂热游戏玩家，每天都在游戏中度过，那么依然**不建议学**。游戏的世界已经足够广阔，没必要难为自己。尽管学习编程语言不难，但也要投入时间。

### 比较复杂的情况

如果你是典型的办公室人员，每天需要处理大量 Word 文档和表格，那么情况就有一些复杂了。

分为两部分：

1. 已经熟悉电脑基本操作和概念，能够用 Word 完成日常任务的人。
2. 不熟悉电脑基础操作，进入职场 = 刚用电脑的人。

对于 1，**可以学，但不是必须学**。如果你有额外的精力，能够投入时间，那么学习编程语言会对你带来很大的收益。具体选择哪一门是很关键的——非计算机专业人士，没必要掌握过于专业的技能。这部分会在下文谈到。学会一门编程语言，你可以自己开发各类使用小工具，面对各种复杂需求，你甚至可以几分钟搞定。

对于 2，**不建议学**。编程语言中有大量的计算机基础知识。比如，**路径**，实际的程序会大量处理路径。下面是一个小测试。

> 对于文件 `D:\files\人员名单` 的说法，正确的是
>
> A. 可以确定 D 盘有一个名为 files 的文件
> B. “人员名单”是一个文档
> C. 这是相对路径格式
> D. 把“人员名单”移动到上一级目录，可得 `D:\人员名单`

如果你不能立即反应出 A B C 都是错的，那么不建议学编程语言。

## 选什么编程语言

我听过有人说可以选择经典的 C 语言，毕竟是全国大学入门计算机的第一门编程语言。但问题是，**我们没必要要求自己学习线性表、栈、队列**等专业知识，我们只是为了**自动化现有的流程**——这是普通人学习编程语言的最大好处。

因此，**Python** 是非常优秀的选择。它有丰富的库和很简单的安装方法，你可以快速把自己的想法付诸实践。

比如，我想要批量地把 `doc` 转成 `PDF` 格式，Python 实现如下（体会复杂性即可，无需理解代码）

```python
# 复制并命令行运行：pip install python-office -U
import office 

path = 'C:/app/workbook'  # path这里，填写你存放word文件的位置，例如：C:/app/workbook
office.word.docx2pdf(path=path) # 转换完成
```

如果选择经典的 C 语言，实现难度过大，代码过长，下面是 C 的“扩展版”语言 C++ 的实现：

```cpp
#pragma   warning(disable:4786) 
#import  "C:\Program Files\Common Files\Microsoft Shared\Office12\mso.dll" \
rename("RGB","_OfficeRGB")         
#import  "C:\Program Files\Common Files\Microsoft Shared\VBA\VBA6\VBE6EXT.OLB" \
    rename("Reference", "ignorethis")
#import   "C:\Program Files\Microsoft Office\Office12\msword.olb " \
    rename("FindText","_FindText")\
    rename("Rectangle","_Rectangle")\
    rename("ExitWindows","_ExitWindows")
#import   "C:\Program Files\Microsoft Office\Office12\MSPPT.OLB"
#import "c:\Program Files\Microsoft Office\Office12\EXCEL.exe" \
    rename("DialogBox","_DialogBox") \
    rename("RGB","_RGB") \
    exclude("IFont","IPicture")
#include <string>
#include <iostream>

int Word2PDF(std::wstring inputFileName,std::wstring outputFileName)  
{
    int nR = 0;
    Word::_ApplicationPtr   pWordApp   =   NULL; 
    Word::_DocumentPtr   pDoc   =   NULL; 
    HRESULT hr;
    BSTR szBstrOutputFileName;

    szBstrOutputFileName=SysAllocString(outputFileName.c_str());    
    hr = pWordApp.CreateInstance(__uuidof(Word::Application)); 
    if(hr!=S_OK) return 1;
    Word::DocumentsPtr   pDocs   =   NULL; 
    pWordApp-> get_Documents(&pDocs);
    if(pDocs==NULL)  nR = 2; goto _RELEASE_APP;
    try
    {
        pDoc = pDocs->Open(&(_variant_t(inputFileName.c_str()))); 
        if(pDoc==NULL) goto _RELEASE_APP;
        pDoc->ExportAsFixedFormat(szBstrOutputFileName,Word::WdExportFormat::wdExportFormatPDF,VARIANT_FALSE,
            Word::WdExportOptimizeFor::wdExportOptimizeForPrint,Word::WdExportRange::wdExportAllDocument,1,1,
            Word::WdExportItem::wdExportDocumentContent,VARIANT_TRUE,VARIANT_TRUE,
            Word::WdExportCreateBookmarks::wdExportCreateNoBookmarks,VARIANT_TRUE,VARIANT_TRUE,VARIANT_FALSE);
        pDoc-> Close(); 
        pDoc.Release(); 
        pDoc = NULL; 
    }catch(...)
    {
        nR = 3;
    }

_RELEASE_APP:
    pWordApp-> Quit(); 
    pWordApp.Release(); 
    pWordApp = NULL; 
    return nR;
}
```
