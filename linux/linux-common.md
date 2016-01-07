#linux常用命令

##帮助
`man 命令`
`tldr 命令` too long, don't read，太长不读。

##查寻与替换

`which` 查看可执行文件的位置  
`whereis` 查看文件的位置  
`locate` 配合数据库查看文件位置  
`find` 实际搜寻硬盘查询文件名称  
从根目录开始查找所有扩展名为.log的文本文件，并找出包含”ERROR”的行  
` find / -type f -name "*.log" | xargs grep "ERROR" `  
例子：从当前目录开始查找所有扩展名为.conf的文本文件，并找出包含”abc”的行  
` find . -name "*.conf" | xargs grep "abc" `  
` sudo find / | grep "关键字" `  
替换  
 ` sudo grep 'abc' -rl /home/plusdo/ | xargs sed -i "s/abc/xyz/g" ` 

##删除

删除.svn文件

```
find . -type d -name '.svn'|xargs rm -rf
```
或

```
find . -type d -i name '.svn' -exec rm -rf {} \;
```
 `-i` 忽略大小写

##修改时区
```
> tzselect 按照提示进行选择时区  
> sudo cp /usr/share/zoneinfo/Asia/ShangHai /etc/localtime  
> sudo ntpdate cn.pool.ntp.org   
cn.pool.ntp.org是位于中国的公共NTP服务器，用来同步时间  
```

##系统
```
# uname -a                 # 查看内核/操作系统/CPU信息
# head -n 1 /etc/issue  # 查看操作系统版本
# cat /proc/cpuinfo      # 查看CPU信息
# hostname               # 查看计算机名
# lspci -tv              # 列出所有PCI设备
# lsusb -tv              # 列出所有USB设备
# lsmod                  # 列出加载的内核模块
# env                    # 查看环境变量
```
##资源
```
# free -m                # 查看内存使用量和交换区使用量
# df -h                  # 查看各分区使用情况
# du -sh <目录名>        # 查看指定目录的大小
# grep MemTotal /proc/meminfo   # 查看内存总量
# grep MemFree /proc/meminfo    # 查看空闲内存量
# uptime                 # 查看系统运行时间、用户数、负载
# cat /proc/loadavg      # 查看系统负载
```
##磁盘和分区
```
# mount | column -t      # 查看挂接的分区状态
# fdisk -l               # 查看所有分区
# swapon -s              # 查看所有交换分区
# hdparm -i /dev/hda     # 查看磁盘参数(仅适用于IDE设备)
# dmesg | grep IDE       # 查看启动时IDE设备检测状况
```
##网络
```
# ifconfig               # 查看所有网络接口的属性
# iptables -L            # 查看防火墙设置
# route -n               # 查看路由表
# netstat -lntp          # 查看所有监听端口
# netstat -antp          # 查看所有已经建立的连接
# netstat -s             # 查看网络统计信息
```
##进程
```
# ps -ef                 # 查看所有进程
# top                    # 实时显示进程状态
```
##用户
```
# w                      # 查看活动用户
# id <用户名>            # 查看指定用户信息
# last                   # 查看用户登录日志
# cut -d: -f1 /etc/passwd   # 查看系统所有用户
# cut -d: -f1 /etc/group    # 查看系统所有组
# crontab -l             # 查看当前用户的计划任务
# passwd username        #修改密码 

```
####添加用户

```sudo adduser plusdo(用户)```

修改`/etc/sudoers`文件
```
# User privilege specification
root    ALL=(ALL:ALL) ALL
plusdo ALL=(ALL:ALL) ALL #此处是将plusdo设置成sudo用户
```

##服务
```
# chkconfig --list       # 列出所有系统服务
# chkconfig --list | grep on    # 列出所有启动的系统服务
```

##参考 

http://www.ha97.com/981.html
