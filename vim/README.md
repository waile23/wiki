#vim
一直用着vim,喜欢vim提供的基本功能，对网上提供的各种插件，各种配置的方式不是特别感兴趣，vim自带的功能都没有都用好,不过多在工具上耽误过多的时间。

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
 
 
" 插入匹配括号
inoremap ( ()<LEFT>
inoremap [ []<LEFT>
inoremap { {}<LEFT>

"map <C-n> :NERDTreeToggle<CR>



```


###vim积累
1. 看完[vim入门](vimtutor.md)基本就可以掌握VIM的基本应用了。
1. 外部剪切板vim外部剪切板
1. vim在编辑过程中的切出与切入
1. vim中关于批量替换的一些技巧
1. vim宏的用法

###vim常用操作


###打开、显示文件
1. vim还没有启动的时候：在终端里输入`shell>vim file1 file2 … filen`便可以打开所有想要打开的文件

1. vim已经启动，输`入:open file`可以再打开一个文件，并且此时vim里会显示出file文件的内容。

同时显示多个文件：`:split`、`:vsplit`

在文件之间切换： 
--* 文件间切换 `Ctrl+6`—下一个文件 
--* `:bn`—下一个文件 
--* `:bp`—上一个文件 


对于用`(v)split`在多个窗格中打开的文件，这种方法只会在当前窗格中切换不同的文件。

1. 在窗格间切换的方法 
--* `Ctrl+w+方向键`——切换到前／下／上／后一个窗格 
--* `Ctrl+w+h/j/k/l` ——同上 
--* `Ctrl+ww`——依次向后切换到下一个窗格中 

####书签
* 建立书签，局部书签`m+[a-z]`和全局书签`m+[A-Z]`。
* 跳转到书签，`'+[a-z]`与`'m+[A-Z]`。


###vim插件
1. vim插件管理器vundle

###vim应用
1. chrome下的vim插件[vimium](vimium.md)
1. eclipse下的vim插件
