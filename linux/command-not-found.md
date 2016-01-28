 #bash: xxx command not found的解决办法

Linux命令行输入命令执行后报“bash:....:command not found”这是由于系统PATH设置问题，PATH没有设置对，系统就无法找到精确命令了。

下面给出2种解决办法

1. 在命令行中输入：`export PATH=/usr/bin:/usr/sbin:/bin:/sbin:/命令的位置` 这样可以保证命令行命令暂时可以使用。命令执行完之后先不要关闭终端。


2. 在命令行中输入 `vi ~/.bashrc`(ubuntu 13.04, 其他型可能是 .bash_profile)

在最底下输入
```
export PATH=$PATH:$HOME/bin:/sbin:/usr/bin:/usr/sbin:/$HOME/zato-bin/zato-1.1/bin
```

回到命令行中输入`sudo su plusdo`，再次执行未找到的命令，就正常了。也可以关闭终端，重新打开终端，输入命令执行。
