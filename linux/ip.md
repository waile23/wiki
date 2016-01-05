#Linux(ubuntu)下设置网络

##以DHCP方式配置网卡

``` 
#sudo vim /etc/network/interfaces
auto lo
iface lo inet loopback
 
auto eth0
iface eth0 inet dhcp #以上表示默认使用DHCP分配IP

``` 

用下面的命令使网络设置生效:
``` 
sudo /etc/init.d/networking restart
``` 

也可以在命令行下直接输入下面的命令来获取地址

``` 
sudo dhclient eth0
``` 
##配置静态IP地址

加入以下语句：
``` 
#sudo vim /etc/network/interfaces
auto eth0
iface eth0 inet static
#iface eth0 inet dhcp
address xxx.xxx.xxx.xxx #IP地址
netmask xxx.xxx.xxx.xxx #子网掩码
gateway xxx.xxx.xxx.xxx #网关
``` 
##修改DNS
``` 
#sudo vim /etc/resolv.conf
添加如下内容（这点所有Linux发行版都通用）：
nameserver 172.16.3.4 希望修改成的DNS
nameserver 8.8.8.8 
``` 

重启networking服务使其生效：
``` 
sudo /etc/init.d/networking restart
#或者
sudo service networking restart
``` 

永久修改网卡DNS

注意：重启Ubuntu后发现又不能上网了，问题出在/etc/resolv.conf。重启后，此文件配置的dns又被自动修改为默认值。所以需要永久性修改DNS。方法如下：
``` 
# vim /etc/resolvconf/resolv.conf.d/base
nameserver 192.168.80.2
nameserver 8.8.8.8
``` 
