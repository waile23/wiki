#常见问题

##mysql客户端连接10061错误

远程使用mysql 客户端软件连接 mySql数据时，连接出现`2003-Can’t connect to MySQL on ’192.168.0.1’(10061)`错误时，是由于MySQL不准许远程连接。

修改方法如下：

1：在服务端MySQL文件夹下找到`my.ini/my.cnf`文件。修改`bind-address=127.0.0.1` 为` bind-address=0.0.0.0`

2：重新启动MySQL服务。


##mysql删除记录时外键错误的问题

在SQLyog中删除一张表时候，出现

`Error No. 1451 Cannot delete or update a parent row: a foreign key constraint fails (…)`

这可能是MySQL在InnoDB中设置了foreign key关联，造成无法更新或删除数据。可以通过设置FOREIGN_KEY_CHECKS变量来避免这种情况。

```
/*删除前设置*/
SET FOREIGN_KEY_CHECKS = 0;
/*执行删除*/
DELETE FROM USER WHERE id=1;
/*删除完成后设置*/
SET FOREIGN_KEY_CHECKS = 1;
```