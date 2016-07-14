#vim

一直用着vim,喜欢vim提供的基本功能，对网上提供的各种插件，各种配置的方式不是特别感兴趣，vim自带的功能都没有都用好,不过多在工具上耽误过多的时间。

###入门
看完[vim入门](vimtutor.md)基本就可以掌握VIM的基本应用了。

###学习
使用`:help`命令其实就可以学习大部分内容，也可以使用`:help subjuect`对进入相关的帮助。

下面是vim中文手册的链接地址，可以直接下载pdf版本学习。

- [vim中文手册](http://vimcdoc.sourceforge.net/)  
- [直接下载](http://sourceforge.net/project/showfiles.php?group_id=56777)  
- [在线学习](http://vimcdoc.sourceforge.net/doc/)
- [中文手册项目地址](http://sourceforge.net/projects/vimcdoc/)  
- [gvim中文帮助](http://sourceforge.net/projects/vimcdoc/files/win32-install/)可替换原英文帮助  


把一些基本的内容记录在这里以备不时之需。

###vim基本设置
下面几个设置可以满足日常需要，缩进主要是为了编写python,nodejs时用的。
```vim
"设置缩进 
set tabstop=4          "设定tab宽度为4个字符
set shiftwidth=4       "设定自动缩进为4个字符
set expandtab          "用space替代tab的输入
set nu                 "显示行号
 
set noexpandtab        "不用space替代tab的输入
set encoding=utf-8     "设置 字符集

setlocal cm=blowfish   "设置Blowfish加密算法
"setlocal cm=blowfish2 " best (requires Vim version 7.4.399 or higher)
 
" 插入匹配括号
inoremap ( ()<LEFT>
inoremap [ []<LEFT>
inoremap { {}<LEFT>

"map <C-n> :NERDTreeToggle<CR> "NERDTree插件的快捷键
```
###vim常用操作
`.` 重复上一次修改，非常好用  
`cw` 替换整个字 和`.`一起使用
`:normal` 统一操作  
`ctrl-o` 在编辑模式下切换到一般模式，输入一个字符，在输入`() '' "" {} []`等打操作时使用很好用  
`gu gU` 大小写转换  
`iw`  
`aw`  
`quickfix`中的命令
`:Ve 20` 按20%的比例打开目录列表， shift+p(大写P)不在当前目录窗口打开文件。  
`*`、`#`搜索当前选中词，高亮显示，与`n`和`N`配合使用向下查找或向上查找。

对标记文本模式中区域选择  
- aw -- 选中一个单词,含单词后的空格  
- as -- 选中一个句子,含句号后的空格  
- ap -- 选中一个段落,含段落后的空格  
- ab -- 选中()括号中的所有内容,含()  
- aB -- 选中{}括号中的所有内容,含{}  
- iw -- 选中一个单词,不含单词后的空格  
- is -- 选中一个句子,不含句号后的空格  
- ip -- 选中一个段落,不含段落后的空格  
- ib -- 选中()括号中的内容,不含()  
- iB -- 选中{}括号中的内容,不含{}  

####c命令
- `c`剪切-进入编辑模式  
- `C`同`c$`  
- `c0`
- `ciw'、`caw`等命令
- `cfx`、`cFx`
- `cc`同`S`



###移动
`w e b ge f t ^ $ 0 hh G` 

`%`匹配`() [] {}`

`CTRL-O` 命令则跳到一个 "较老" 的地方 (提示: O 表示 older)。`CTRL-I` 则跳到一个 "较新" 的地方 (提示: I 在键盘上紧靠着O)。



             |  example text   ^             |
        33G  |  example text   |  CTRL-O     | CTRL-I
             |  example text   |             |
             V  line 33 text   ^             V
             |  example text   |             |
       /^The |  example text   |  CTRL-O     | CTRL-I
             V  There you are  |             V
                example text



###翻页 

整页翻页`ctrl-f ctrl-b`,`f`就`是forword` `b`就是`backward`。

翻半页`ctrl-d ctlr-`  `d=down u=up`

滚一行`ctrl-e ctrl-y`

`zz`让光标所杂的行居屏幕中央  
`zt`让光标所杂的行居屏幕最上一行`t=top` 
`zb`让光标所杂的行居屏幕最下一行`b=bottom` 


###查找与替换

[查找和替换](vim查找和替换.md)

###vim外部剪贴板

普通列表项目查看是否可以使用外部剪切板 `vim –version | grep xterm_clipboard`  
`sudo apt-get install vim-gnome`就可以使用了 15M左右  
`”+y` 和 `”+p` 复制和粘贴。  
`:reg` 查看寄存器， 看到的内容类似 `“0、“1、”+、“/` 等，那么只要输入 `“0p、“1p、”+p、“/p` 就可以将寄存器的内容粘贴到vim中了。  

###Explore
`Ve 20`显示vim文件目录结构，定位文件后`P(大写)`，在新窗口的打开文件。

已经使用`NERDTree`插件代替。

###打开、显示文件
1. vim还没有启动的时候：在终端里输入`shell>vim file1 file2 … filen`便可以打开所有想要打开的文件

1. vim已经启动，输`入:open file`可以再打开一个文件，并且此时vim里会显示出file文件的内容。

同时显示多个文件：`:split`、`:vsplit`

在文件之间切换： 
--* 文件间切换 `CTRL+6`—下一个文件  
--* `:bn`—下一个文件  
--* `:bp`—上一个文件  
对于用`(v)split`在多个窗格中打开的文件，这种方法只会在当前窗格中切换不同的文件。  

1. 在窗格间切换的方法  
--* `CTRL+w+方向键`——切换到前／下／上／后一个窗格  
--* `CTRL+w+h/j/k/l` ——同上  
--* `CTRL+ww`——依次向后切换到下一个窗格中  
--* `CTRL+w+=/+/-`——处理窗格的大小  

###缓冲区文件
- ｀:ls, :buffers ｀               列出所有缓冲区
- ｀:bn[ext]   ｀                  下一个缓冲区
- ｀:bp[revious]｀                 上一个缓冲区
- ｀:b {number, expression}｀      跳转到指定缓冲区

###宏
在Normal模式下，按`qa`（q表示开始录制宏，宏的名字为a，也可以是b,c…）开始录制。  
输入要操作的内容，正常的vim功能。  
esc回到Normal模式下，再按`q`结束宏录制。  
使用：Normal模式下，`@a`执行宏，输入`n@a`执行n次该宏a的内容，如`5@a`。  

###书签
* 建立书签，局部书签`m+[a-z]`和全局书签`m+[A-Z]`。
* 跳转到书签，`'+[a-z]`与`'m+[A-Z]`。

###补全
`CTRL+p`和`CTRL+n`弹出补全列表，再按`CTRL+p`和`CTRL+n`进行向上和向下选择。

其他补全方式  

```
整行补全                        CTRL-X CTRL-L
根据当前文件里关键字补全        CTRL-X CTRL-N
根据字典补全                    CTRL-X CTRL-K
根据同义词字典补全              CTRL-X CTRL-T
根据头文件内关键字补全          CTRL-X CTRL-I
根据标签补全                    CTRL-X CTRL-]
补全文件名                      CTRL-X CTRL-F
补全宏定义                      CTRL-X CTRL-D
补全vim命令                     CTRL-X CTRL-V
用户自定义补全方式              CTRL-X CTRL-U
拼写建议                        CTRL-X CTRL-S 
```

###加密

- 编辑模式，输入`:X（大写）`，回车。
- `$vim -x`启动文件是加密。

vim7.3版本支持两种加密方式——PKzip算法（已知有缺陷的）、Blowfish算法（从7.3版本开始支持）。  
vim7.4版本支持Blowfish2算法。  
vim -x 默认采用PKzip算法加密。  
以通过`:setlocal cm=blowfish`设置加密算法。  



###vim插件
1. vim插件管理器vundle
1. NERDTree  
`C（大写 C ）`将光标所在目录设置为根目录。

###vim应用
1. chrome下的vim插件vimium
1. eclipse下的vim插件  
1. nodepad++下的vim插件[visimulator](visimulator.zip)  


###解决gvim中文乱码的问题
```
set guifont=Consolas:h12:cANSI
set encoding=utf-8
set fileencodings=utf-8,chinese
set termencoding=utf-8
if has("win32")
set fileencoding=chinese
else
set fileencoding=utf-8
endif
"解决菜单乱码
source $VIMRUNTIME/delmenu.vim
source $VIMRUNTIME/menu.vim
"解决consle输出乱码
language messages zh_CN.utf-8
```
