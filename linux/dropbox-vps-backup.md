#利用dropbox备份vps上的文件与数据
##通过命令行安装 Dropbox

Dropbox 守护程序可在所有 32 位与 64 位 Linux 服务器上正常运行。若要安装，请在 Linux 终端运行下列命令。

32-bit:
```
cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86" | tar xzf -
```
64-bit:
```
cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -
```
接着，从新建的 .dropbox-dist 文件夹运行 Dropbox 守护程序。
```
~/.dropbox-dist/dropboxd
```

如果是首次在服务器上运行 Dropbox，系统会要求您将链接复制并粘贴到运行的浏览器中，以便创建一个新的帐户或将服务器附加到现有帐户上。操作完成后，系统会在您的主目录中创建 Dropbox 文件夹。下载这个 [CLI脚本](https://www.dropbox.com/download?dl=packages/dropbox.py)，以便从命令行控制 Dropbox。为了方便访问，请在 PATH 中的任何地方放入该脚本的符号连接。

##编写shell运行同步
```
#!/bin/bash
#waile23@163.com
#auto backup, auto sync dropbox
echo 处理sudo 命令
echo 'your password' | sudo -S pwd
#sudo -i
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
export PATH

echo 需要备份的路径
backup_path="/var/www /etc/apache2"
echo 需要备份的文件名
nowdate=`date +%y%m%d%H%M%S`
backup_file="vps_backup_${nowdate}.tar.gz"
echo dropbox在本机的同步目录
dropbox_sync_path="/home/plusdo/Dropbox/"

echo $backup_path
echo $backup_file
echo $dropbox_sync_path

echo 进入Dropbox同步目录，打包需要备份的文件到Dropbox同步目录中
cd $dropbox_sync_path &&  sudo tar -zpcv -f $backup_file $backup_path

#~/.dropbox-dist/dropboxd
exit 0
```

利用 [crontab](crontab.md)来做定时任务。

shell可以自行处理，如处理数据库备份等。

##相关资源
[Dropbox命令行下安装与维护](http://salogs.com/2010/06/ubuntudropbox-e5-91-bd-e4-bb-a4-e8-a1-8c-e4-b8-8b-e5-ae-89-e8-a3-85-e4-b8-8e-e7-bb-b4-e6-8a-a4/)
