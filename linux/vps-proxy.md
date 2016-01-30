通过vps进行ssh代理上网

```
ssh -qTfnN -D 7070 user@host -p port

说明: user是你的帐号,host指对方linux主机的ip
-q Quiet mode. 安静模式，忽略一切对话和错误提示。
-T Disable pseudo-tty allocation. 不占用 shell 了。
-f Requests ssh to go to background just before command execution. 后台运行，并推荐加上 -n 参数。
-n Redirects stdin from /dev/null (actually, prevents reading from stdin). -f 推荐的，不加这条参数应该也行。
-N Do not execute a remote command. 不执行远程命令，专为端口转发度身打造。
```

##windows下使用putty代理
http://www.renhaibo.com/archives/152.html


##使用putty进行代理

