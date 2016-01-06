#apache

###开启rewrite模块

RewriteEngine命令需要`rewrite mod`的支持
```
$>cd /etc/apache2/mods-available 切换到apache下的mods-available目录
$>sudo vim rewrite.load 将#LoadModule rewrite_module modules/mod_rewrite.so前的#去掉
$>cd /etc/apache2/mods-enabled 切换到apache下的mods-enabled目录
$>sudo ln -s ../mods-available/rewrite.load rewrite.load 启用rewrite mod
$>sudo /etc/init.d/apache2 restart 重启apache服务器。
```


###a2enmod a2ensite

###ab测试
[ab测试](ab.md)

###apache prefork 模块指令分析

###mod_status模块

打开apache状态监控

1. 修改conf/httpd.conf文件，
```
将#LoadModule status_module modules/mod_status.so前#去掉，打开状态监控报告。
修改成如下：
LoadModule status_module modules/mod_status.so

将#Include conf/extra/httpd-info.conf前#去掉，使得 httpd-info.conf 生效
修改成如下：
Include conf/extra/httpd-info.conf
```

2. 修改conf/extra/httpd-info.conf文件设置状态监控访问的地址
```
打开conf/extra/httpd-info.conf文件
原来内容：
<Location /server-status>
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from .samsungservice.com.cn
</Location>
修改成如下：
 
<Location /server-status>
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from all
</Location>
```
3. 查看apache状态监控信息 在浏览器地址栏输入：`http://Apache IP 地址/server-status`


###mod_evasive防止ddos

###apache下waf-ModSecurity
