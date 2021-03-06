#vim查找和替换

##单文件查找和替换

###查找

`/pattern<Enter>` ：向下查找pattern匹配字符串   
`?pattern<Enter>`：向上查找pattern匹配字符串  
使用了查找命令之后，使用如下两个键快速查找：  
`n`：按照同一方向继续查找  
`N`：按照反方向查找  

####多选一查找
`/foo\|bar` 这个命令匹配了 "foo" 或 "bar"。

####单行查找
`f`	向前搜索并将光标停留在目标字符上  
`F`	向后搜索并将光标停留在目标字符上  
`;`	重复刚才的查找  
`,`	反向重复刚才的查找  
`t`	向前搜索并将光标停留在目标字符的前一个字符上  
`T`	向后搜索并将光标停留在目标字符的后一个字符上  

###替换
`:[addr]s/源字符串/目的字符串/[option]`

`[addr]` 表示检索范围，省略时表示当前行。  
`1，20`  ：表示从第1行到20行;   
`%` ：表示整个文件，同`1,$`;   
`. ,$` ：从当前行到文件尾。

`s` : 表示替换操作  

`[option]` : 表示操作类型  
`g` 表示全局替换;   
`c` 表示进行确认; 
`p` 表示替代结果逐行显示（Ctrl + L恢复屏幕）;   
省略`option`时仅对每行第一个匹配串进行替换。 

##多文件查找和替换
  
       
###查找

`:vim[grep][!] /{pattern}/[g][j] {file} ...`  
`:vimgrep word *` 目录查找word  
`:vimgrep word **` 所有下级目录查找word  
`g` 和 `j` 是两个可选的标志位，g表示是否把每一行的多个匹配结果都加入。j表示是否搜索完后定位到第一个匹配位置。    
要搜索的文件 可以是具体的文件路径，也可以是带通配符的路径比如 `*.as **/*.as` ，`**`表示递归所有子目录。 要搜索的文件和或搜索范围都可 以写多个，用空格分开。    

`:cw` 打开quickfix列表  
`:cn` 下一个匹配位置  
`:cp` 上一个匹配位置  
`:cl` 查看所有匹配的位置    

###替换

实际上只要如下两个命令即可（假设要将当前目录下所有扩展名为.txt/.cpp的文件中的hate替换成love）:

```
:args *.txt *.cpp 扫描当前目录下的.txt 和 .cpp文件，并加入到参数列表。  

:argdo %s/hate/love/gc | update 是将参数列表中的所有文件的hate提换成love，并写入硬盘。  
```


如果想要递归扫描所有下级目录的话，用  
`:args **/*.txt`  
如果只想扫描下一级目录（即不扫描当前目录）的话，用  
`:args */*.txt`  

####替换示例
在mactalk中看到的一些技巧。

每一行文字前增加“序号.”，可以执行下面的命令。

`:let i=1 | g/^/ s//\=i."."/ | let i +=1`

如果想把当前目录下（包括子文件夹）所有后缀为java的文件中的apache替换成eclipse，那么可以在当前目录下依次执行如下命令。
```
:n */.java
:argdo %s/apache/eclipse/ge |update
```
从上述替换命令可以看到：g 放在命令末尾，表示对搜索字符串的每次出现进行替换；不加 g，表示只对搜索

字符串的首次出现进行替换；g 放在命令开头，表示对正文中所有包含搜索字符串的行进行替换操作。



##参考
http://blog.csdn.net/lanxinju/article/details/5731843  
http://wdicc.com/search-in-vim/  
http://dingxd04.blog.163.com/blog/static/23656662012101682550668/  
http://www.vimer.cn/2009/10/vimgvim%E5%AE%9E%E7%8E%B0%E5%A4%9A%E6%96%87%E4%BB%B6%E7%9A%84%E6%9F%A5%E6%89%BE%E5%92%8C%E6%9B%BF%E6%8D%A2.html  
