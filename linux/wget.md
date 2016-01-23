#wget

wget是一个从网络上自动下载文件的自由工具，支持通过HTTP、HTTPS、FTP三个最常见的TCP/IP协议下载，并可以使用HTTP代理。wget名称的由来是“World Wide Web”与“get”的结合。

只采用wget做下载用，其他可以使用crul代替。


```
#下载ftp下的文件及目录
wget -c -r -np -l 0 ftp://user:password@192.168.1.1/path
```

