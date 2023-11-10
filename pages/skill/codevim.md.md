# 在VSCode里面配置Vim的正确姿势

*来自 https://zhuanlan.zhihu.com/p/188499395 and https://zhuanlan.zhihu.com/p/512935904*

在vscode的扩展商店中搜索vim，安装第一个插件，这个插件可以完成大部分原生vim的操作。

安装完成以后我们需要配置vim，原生的vim有一部分操作十分的不友好，我们常常需要改键配置合适自己的vim。我们通常在setting.json中配置vscode，如果不知道如何打开setting.json可以点开文件->首选项->设置->文本编辑器，向下拉找到“在setting.json中编辑”

`vim.commandLineModeKeyBindingsNonRecursive`指的是命令行模式非递归键位绑定，在原生vim中等同于norecmap。
`vim.insertModeKeyBindings`指的是插入模式下键位绑定，在原生vim里面指的是imap。
`vim.normalModeKeyBindingsNonRecursive`指的是普通模式下非递归键位绑定，在原生vim中是noremap。

我这里把esc键映射为jj，意思是在插入模式下，按下两次j会回到正常模式、按下大写s可以保存当前文件、按下大写q可以关闭当前文件。这vim的配置文件中，可以兼容原生vim指令和vscode命令，"workbench.action.files.save" 属于vscode命令，":q!" 属于原生vim命令。如果想修改其他键位可以根据下面的语法规则进行修改测试。

```json
"vim.insertModeKeyBindings": [
        {
            "before": ["j", "j"],
            "after": ["<Esc>"]
        }
    ],
```

这里我通过按下leader键+s 可以保存当前文件、按下leader+q关闭文件、按下leader+sq 保存并退出文件。在下面我会提到leader键的设置。

```json
 "vim.normalModeKeyBindingsNonRecursive": [
        {
            "before": ["<leader>", "s"],
            "commands":[":w!"]
        },
        {
            "before": ["<leader>", "q"],
            "commands":[":q!"]
        },  
        {
            "before": ["<leader>", "sq"],
            "commands":[":wq!"]
        }
    ],
```

leader键位设置和取消vim键位映射

leader在vim中的意思是“前缀”的意思，和tmux中的Ctrl+b是一个意思，可以通过自定义leader键，来构建自己需要的组合快捷键。

在这里我把leader键位映射为空格键`<space>`。

在vscode里面使用vim有时候vscode原生键位比vim原生键位要舒服一些，我们可以取消到vim里面的键位映射来使用vscode的键位。

比如下面我取消掉了Ctrl+a,Ctrl+f,Ctrl+n在vim中的键位映射，这样子在写代码的时候，我按下Ctrl+A,Ctrl+F,Ctrl+N就可以使用vscode中的全选，查找和新建。

```json
 "vim.leader": "<space>",
 "vim.handleKeys": {
        "<C-a>": false,
        "<C-f>": false,
        "<C-n>": false
}
```

**复制/粘贴**

在 Normal 模式下，复制是 y ，粘贴是 p 。例如，复制当前行使用 yy，光标移动到指定位置，按下 p 后被复制的内容会出现在光标下一行。在 Insert 模式下，快捷键 Ctrl+r加上寄存器的标识可以从任何有标识的寄存器粘贴内容。这些都是 Vim 中的基本知识，更多的复制/粘贴技巧，可以参考 Vim 的相关教程，此处就不做过多的阐述了。

**撤销 / 反撤销**

在 Normal 模式下，使用 u 可以撤销上一步 Vim 操作，使用 Ctrl+r 可以撤销上一步的撤销。在 Insert 模式下，Ctrl+z 和 Ctrl+Shift+z 也是可以使用的，但是不建议大家这样做，因为在 Vim 中这两个快捷键代表了其他操作。

**内容查找**

在 Normal 模式下，使用 /+内容 或 ?+内容 在当前文件中查询 内容。然后使 n 或 N 跳转至下一个或上一个内容匹配处，当然，你也可以使用 <leader>+<C-f>（已经重新映射了）。如果是整个项目下查询内容，此时我还是在用 VS Code 下的快捷键 Ctrl+Shift+f 进行查询。

**Tab切换**
使用 gt (go tab) 切换至下一个 Tab，gT 切换至上一个 Tab，使用 n+gt 切换至第 n 个 Tab。当然，你可以使用 VS Code 的快捷键 Alt+n 切换至第 n 个 Tab。

**代码注释**
使用 gcc 注释当前行，再次 gcc 可以取消注释。当然，你可以使用 VS Code 的快捷键 Ctrl+/ 进行注释和取消注释。

**跳转代码定义处 / 跳转代码引用处**

使用 gd (go definition) 可以快速跳转至代码定义处或代码引用处，相当于按下 Ctrl+鼠标左键 的效果。ctrl+] 返回

**显示代码文档信息**

使用 gh 可以查看代码文档信息，相当于鼠标悬停在代码上面的效果。

**新建窗口**

使用 Ctrl+w v 新建垂直窗口，Ctrl+w s 新建水平窗口。使用 Ctrl+w h、Ctrl+w j、Ctrl+w k、Ctrl+w l 在窗口间进行切换。使用 Ctrl+w o 关闭除当前窗口外的其他窗口。另外需要注意的是，Vim 中的 Tab 和窗口概念和我们平时使认知的 Tab 和窗口还是有点区别的，具体可查询 Vim 相关教程。