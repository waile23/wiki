MySQL的字符集支持(Character Set Support)有两个方面：字符集(Character set)和排序方式(Collation)。    
对于字符集的支持细化到四个层次: 服务器(server)，数据库(database)，数据表(table)和连接(connection)。    

##查看字符集
```
mysql> show variables like 'character%';
mysql> show variables like 'collation_%';
```

1.修改配置文件：    
```
shell> vi /etc/mysql/my.cnf     
[client]     
default-character-set=utf8     
[mysql]    
default-character-set=utf8    
[mysqld]    
collation-server = utf8_unicode_ci    
init-connect=’SET NAMES utf8′    
character-set-server = utf8
```  

2.修改数据库： 
```
mysql>ALTER DATABASE db_name DEFAULT CHARACTER SET character_name [COLLATE ...];     
```

3.把表默认的字符集和所有字符列（CHAR,VARCHAR,TEXT）改为新的字符集：    
```
 mysql>ALTER TABLE tbl_name CONVERT TO CHARACTER SET character_name [COLLATE ...]   
 mysql>ALTER TABLE logtest CONVERT TO CHARACTER SET utf8 COLLATE utf8_general_ci;     
```

只是修改表的默认字符集：     
```

 mysql>ALTER TABLE tbl_name DEFAULT CHARACTER SET character_name [COLLATE...];    
 mysql>ALTER TABLE logtest DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;   
``` 

4.修改字段的字符集：    
```
 mysql>ALTER TABLE tbl_name CHANGE c_name c_name CHARACTER SET character_name [COLLATE ...];    
 mysql>ALTER TABLE logtest CHANGE title title VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci;   
``` 

5.临时更改连接字符集：
```
mysql> SET NAMES utf8;    
```

查看数据库的字符集  
```  
mysql> show create database test; 
```

查看表的字符集,包括各个字段的字符集,如果各字段没有标明,表示与表的字符集一致    

``` 
mysql> show create table books    
```

查看字段编码   
```
SHOW FULL COLUMNS FROM tbl_name;    
```
