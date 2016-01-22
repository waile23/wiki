#wget

只采用wget做下载用，其他可以使用crul代替。


```
#下载ftp下的文件及目录
wget -c -r -np -l 0 ftp://user:password@192.168.1.1/path
```

