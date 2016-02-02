#mysql 赋给用户权限 grant all privileges on

```
GRANT ALL PRIVILEGES ON *.* TO 'myuser'@'%' IDENTIFIED BY 'mypassword' WITH GRANT OPTION;  
FLUSH   PRIVILEGES; 
``` 
 
如果你想允许用户myuser从ip为192.168.1.6的主机连接到mysql服务器，并使用mypassword作为密码 

```
GRANT ALL PRIVILEGES ON *.* TO 'myuser'@'192.168.1.3' IDENTIFIED BY 'mypassword' WITH GRANT OPTION;   
FLUSH   PRIVILEGES; 
```



如果你想允许用户myuser从ip为192.168.1.6的主机连接到mysql服务器的dk数据库，并使用mypassword作为密码 
```
GRANT ALL PRIVILEGES ON dk.* TO 'myuser'@'192.168.1.3' IDENTIFIED BY 'mypassword' WITH GRANT OPTION; 
FLUSH   PRIVILEGES; 
```


注意授权后必须`FLUSH PRIVILEGES;`否则无法立即生效。 


另外一种方法，在安装mysql的机器上运行： 
```
1、d:\mysql\bin\>mysql -h localhost -u root 

2、mysql>SET SESSION sql_mode='STRICT_TRANS_TABLES,NO_ENGINE_SUBSTITUTION'; 
//这样应该可以进入MySQL服务器 
3、mysql>GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;

//赋予任何主机访问数据的权限 
4、mysql>FLUSH PRIVILEGES ;
//修改生效 
5、mysql>EXIT 
//退出MySQL服务器 
```
这样就可以在其它任何的主机上以root身份登录啦！


##说明

SQL服务器模式

模式定义MySQL应支持哪些SQL语法，以及应执行哪种数据验证检查。你可以用SELECT @@sql_mode语句查询当前的模式。

NO_AUTO_CREATE_USER,防止GRANT自动创建新用户，除非还指定了密码。

你还可以在启动后用SET [SESSION|GLOBAL] sql_mode='modes'语句设置sql_mode变量来更改SQL模式。

设置 GLOBAL变量时需要拥有SUPER权限，并且会影响从那时起连接的所有客户端的操作。设置SESSION变量只影响当前的客户端。

任何客户端可以随时更改自己的会话 sql_mode值。
 

原来是设定了 sql 服务器模式。 sql_mode值 是保存在 my.ini 中，可以直接打开该文件修改后再重启服务，也可以用SET SESSION sql_mode='STRICT_TRANS_TABLES,NO_ENGINE_SUBSTITUTION' 进行更改。


转载至[此处](http://junix1988.iteye.com/blog/309721)