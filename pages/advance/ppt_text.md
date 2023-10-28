# 将PPT中所有文本框里的文字提取出来

打开PPT，按`ALT+F11`打开`VBA`编辑器，在左面的工程视图里点击右键，选择**插入**->**模块**，添加一个模块，名字都不用改。

## 立即执行版

将下列代码贴到刚建立的模块里，按`F5`即可执行`Sub Main()`。运行后，会在 D:\ppt.txt 生成一个文本文件，里面就是所有文本框里的文字。

```vb
Sub Main()
   On Error Resume Next
   Dim allText As String, tmpShape As Shape, tmpSlide As Slide
   allText = ""
   For Each tmpSlide In ActivePresentation.Slides
      For Each tmpShape In tmpSlide.Shapes
         allText = allText + tmpShape.TextFrame.TextRange.Text
         allText = allText + vbCrLf
      Next tmpShape
   Next tmpSlide
   Clipboard.Clear
   Clipboard.SetData allText
   Open "D:\ppt.txt" For Output As #1
   Print #1, allText
   Close #1
   MsgBox Len(allText) & " Written to clipboard and D:\ppt.txt"
End Sub
```

## Word 格式版

鉴于大多数人不会用文本文档，也很难找到 D:\ppt.txt 这个文件，网上有教程是直接导出到 Word 中。这更符合大多数读者的使用习惯。

以下是导出到 Word 版，需要点击顶部的“**工具**”菜单，选择引用，在一大堆选项中找到`Microsoft Word X.0 Object Library`（其中X与你的OFFICE版本有关），**钩上**，点确定。

F5运行后会打开一个word，另存为即可。

```vb
Sub Main()
   On Error Resume Next
   Dim wordApp As New Word.Document, tmpShape As Shape, tmpSlide As Slide
   For Each tmpSlide In ActivePresentation.Slides
   For Each tmpShape In tmpSlide.Shapes
      wordApp.Range().Text = wordApp.Range() + tmpShape.TextFrame.TextRange.Text
      Next tmpShape
      Next tmpSlide
wordApp.Application.Visible = True
End Sub
```

此方法需要额外翻找引用，我觉得很麻烦，故根据这段程序改出了第一个直接导出文本文档的程序。