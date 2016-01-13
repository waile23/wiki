#putty常用

在windows平台下没有其他太好的选择

##配色方案
[solarized配色方案](https://github.com/brantb/solarized/tree/master/putty-colors-solarized)

首先在保存一个session信息，会在putty.exe根目录创建sessions目录，在对应的文件中找到类似部分并替换。

dark版本  
```
Colour21\253,246,227\
Colour20\238,232,213\
Colour19\147,161,161\
Colour18\42,161,152\
Colour17\108,113,196\
Colour16\211,54,130\
Colour15\131,148,150\
Colour14\38,139,210\
Colour13\101,123,131\
Colour12\181,137,0\
Colour11\88,110,117\
Colour10\133,153,0\
Colour9\203,75,22\
Colour8\220,50,47\
Colour7\0,43,56\
Colour6\7,54,66\
Colour5\238,232,213\
Colour4\0,43,54\
Colour3\7,54,66\
Colour2\0,43,54\
Colour1\147,161,161\
Colour0\131,148,150\
```
light版本

```
Colour21\253,246,227\
Colour20\238,232,213\
Colour19\147,161,161\
Colour18\42,161,152\
Colour17\108,113,196\
Colour16\211,54,130\
Colour15\131,148,150\
Colour14\38,139,210\
Colour13\101,123,131\
Colour12\181,137,0\
Colour11\88,110,117\
Colour10\133,153,0\
Colour9\203,75,22\
Colour8\220,50,47\
Colour7\0,43,54\
Colour6\7,54,66\
Colour5\101,123,131\
Colour4\238,232,213\
Colour3\238,232,213\
Colour2\253,246,227\
Colour1\88,110,117\
Colour0\101,123,131\
```

##在putty中输入中文的方法：

缺省情况下，putty对中文的支持却让人不敢恭维，如果远程linux的locale设置为zh_CN.*(bg2312,gbk,utf8等等），显示就是乱码。  
打开putty主程序，选择window-〉Appearance-〉Font settings-〉Change…,选择Fixedsys字体,字符集选择CHINESE_GB2312。 在window-〉Appearance-〉Translation中，Received data assumed to be in which character set 中,把Use font encoding改为UTF-8。  
如果经常使用,把这些设置保存在session里面。  

##pscp.exe
使用方法同linux下的`scp`命令。
