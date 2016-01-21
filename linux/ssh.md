#ssh相关


##修改ssh端口

```
#打开文件/etc/ssh/sshd_config文件  
#sudo vim /etc/ssh/sshd_config 
 
#找到Port 22
#Port 22
Port 2222 #新的端口

#注意：如果不注释Port 22的话，则认为2222端口是新增端口，那么22和2222均可用。
```

重新启动sshd服务  

```
sudo /etc/init.d/sshd restart
```