#chomd命令
* 使用权限 : 所有用户  
* 使用方式 : chmod [-cfvR] [--help] [--version] mode file...

说明 : Linux/Unix 的文件调用权限分为三级 : 文件拥有者[属主]、属组、其他用户。利用 chmod 可以控制文件如何被他人所调用。  

与chmod相关的命令：chown,umask。

##参数
###-cfvR
  - -c : 若该文件权限确实已经更改，才显示其更改动作
  - -f : 若该文件权限无法被更改也不要显示错误讯息
  - -v : 显示权限变更的详细资料
  - -R : 对目前目录下的所有文件与子目录进行相同的权限变更  （常用） 

###mode
权限设定字串，格式如下 : [ugoa...][[+-=][rwxX]...][,...]，其中

- u 表示该文件的拥有者[user]，  
- g 表示与该文件的拥有者属于组(group)，  
- o 表示其他用户[other]，  
- a 表示这三者皆是[all]。（常用）  
  
- + 表示增加权限、（常用）  
- - 表示取消权限、（常用）  
- = 表示唯一设定权限。  
  
- r 表示有可读取的权限，  
- w 表示有可写入的权限，  
- x 表示有可执行的权限，  
- X 表示只有当该文件是个子目录或者该文件已经被设定过为可执行。  

    r=4，w=2，x=1  
    rwx属性则4+2+1=7  
    rw-属性则4+2=6  
    r-x属性则4+1=5  


###示例

```
#给file的属主分配读、写、执行(7)的权限，给file的所在组分配读、执行(5)的权限，给其他用户分配执行(1)的权限

chmod 751 file   

#上例的另一种形式

chmod u=rwx,g=rx,o=x file 
```

#为所有用户分配读权限 ,下面三个相同

chmod =r file 
               　　　　
chmod 444 file 

chmod a-wx,a+r file

#给文件修改所有为所有人可读权限：

chmod ugo+r file

#或

chmod a+r file


#给文件修改所有为所有人可执行权限：  
chmod a+x file

#给文件修改所有为文件属主用户可执行权限：  
chmod u+x file

#把dic目录下的文件设置为所有人可执行权限：  
chmod -R a+x dic/

#把dic目录下的文件全部设置为755权限：  
chmod -R 755 dic/

#取消dic目录下的所有文件可写权限：  
chmod -R a-w  dic/
```
###来源

http://www.linuxyw.com/a/wenjianguanli/20130429/148.html
http://www.cnblogs.com/peida/archive/2012/11/29/2794010.html
