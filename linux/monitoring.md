#linux 监控工具

##系统自带
* 静态进程查看命令（ps）
* 动态进程查看命令（top）
* 查看进程树命令(pstree)

##ps
静态进程查看命令（ps）
```
ps -aux       #查看系统所有进程
ps -lA        #查看所有系统的数据
ps axjf       #连通部分进程树状态

     -A：与-e意思一样，表列出所有进程
     -a ：不与terminal有关的进程
     -u：有效用户相关的进程
      x：通常与a这个参数一起用，可以列出完整信息
输出格式： l：较仔细列出该pid信息
          j：工作格式
          -f：做一个更为完整的输出
```

##top

动态进程查看命令（top）

```
$ top [-d | -bnp]   
-d：表示界面刷新时间，单位秒，默认是5秒   
-b：以批次的方式进行top，还有更多的参数可以使用   
    通常会搭配数据重定向来讲批处理的结果输出成为文件   
-n：与-b搭配，意思是需要进行几次top的输出结果   
-p：查看直接进程，后面接进程号   
  ?：显示在top当中可以输入的按键命令   
  P：以cpu使用率来排名   
  M：以内存的使用率来排名   
  N：以PID来排名   
  T：以进程使用CPU时间累加排名   
  k：给予某个PID一个信号   
  r：给予某个PID重新制定一个nice值   
  q：退出离开 </span>  
```

##pstree
查看进程树命令(pstree)
```
pstree [-A|U] [-up]   
-A：各进程间连接用ASCII字符连接   
-U：该进程之间连接用utf8字符连接   
-p：同时显示PID   
-u：同时列出每个进程的所属账号名称
```

##htop
htop是一款交互式进程查看器
```
$ sudo apt-get install htop
```

##iotop
iotop是IO实时监控器。使用它们附属的详细输入输出（IO）使用方法可以展示出你系统中每个进程线程的信息。
```
$ sudo apt-get install iotop
```

##apachetop
Apachetop展示Apache web服务器上关于http请求的实时表。

它显示统计（stats）, 点击（hits）, 请求（requests）, 请求细节（request details），且能够获得当前你的web服务器正在运行程序的概貌。

```
$ sudo apt-get install apachetop
```

##Glances
Glances是基于CLI curses库的监控工具，Glances用各个分离的表列展示了你机器当前正运行的各种有用的实时数据。Glances旨在用最小的空间显示尽可能多的信息，我认为它的目标完全达到了。
Glances用有限的交互可能性和更深层的信息监控PerCPU, Load, Memory, Swap, Network, Disk i/O, Mount data 和processes，但对于获得一个整体概貌绝对是完美的。
```
$ sudo apt-get install glances
```

转载置http://blog.jobbole.com/58003
