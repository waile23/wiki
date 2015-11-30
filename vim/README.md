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

```


###vim积累
1. 看完[vim入门](vimtutor.md)基本就可以掌握VIM的基本应用了。
1. chrome下的vim插件[vimium](vimium.md)
1. 打开多个文件、同时显示多个文件、在文件之间切换，vim打开文件
1. 外部剪切板vim外部剪切板
1. eclipse下的vim插件
1. vim在编辑过程中的切出与切入
1. vim中关于批量替换的一些技巧
1. vim宏的用法
1. vim插件管理器vundle



