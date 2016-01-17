#crontab

crontab 是用来让使用者在固定时间或固定间隔执行程序之用，换句话说，也就是类似使用者的时程表。-u user 是指设定指定 user 的时程表，这个前提是你必须要有其权限(比如说是 root)才能够指定他人的时程表。如果不使用 -u user 的话，就是表示设定自己的时程表。
```
crontab file [-u user]-用指定的文件替代目前的crontab。
 
crontab-[-u user]-用标准输入替代目前的crontab.
 
crontab-1[user]-列出用户目前的crontab.
 
crontab-e[user]-编辑用户目前的crontab.
 
crontab-d[user]-删除用户目前的crontab.
 
crontab-c dir- 指定crontab的目录。
 
crontab文件的格式：M H D m d cmd.
  * M: 分钟（0-59）。
  * H：小时（0-23）。
  * D：天（1-31）。
  * m: 月（1-12）。
  * d: 一星期内的天（0~6，0为星期天）。
  * cmd要运行的程序，程序被送入sh执行，这个shell只有USER,HOME,SHELL这三个环境变量
```

##crontab示例
[Linux 中 crontab 详解及示例](http://www.cn-java.com/www1/?uid-560221-action-viewspace-itemid-8377)
[hcrontab命令详解](http://bbs.chinaunix.net/forum.php?mod=viewthread&tid=271992)
