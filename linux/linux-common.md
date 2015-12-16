#linux常用命令



##linux下的查询命令

`which` 查看可执行文件的位置  
`whereis` 查看文件的位置  
`locate` 配合数据库查看文件位置  
`find` 实际搜寻硬盘查询文件名称  
从根目录开始查找所有扩展名为.log的文本文件，并找出包含”ERROR”的行  
` find / -type f -name "*.log" | xargs grep "ERROR" `  
例子：从当前目录开始查找所有扩展名为.conf的文本文件，并找出包含”abc”的行  
` find . -name "*.conf" | xargs grep "abc" `  
` sudo find / | grep "关键字" `  



##修改时区

> tzselect 按照提示进行选择时区  
> sudo cp /usr/share/zoneinfo/Asia/ShangHai /etc/localtime  
> sudo ntpdate cn.pool.ntp.org   
cn.pool.ntp.org是位于中国的公共NTP服务器，用来同步时间  
