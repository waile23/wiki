## Redhat配置

###  网络配置
使用`ip addr`查看网络信息

配置路径 `/etc/sysconfig/network-scripts/ifcfg-enp0s3`

```
TYPE=Ethernet
BOOTPROTO=none
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=enp0s3
UUID=27047375-91c2-47a5-95ec-6a9437c579c6
DEVICE=enp0s3
ONBOOT=yes
IPADDR=192.168.187.131
PREFIX=24
GATEWAY=192.168.187.1
DNS1=202.98.0.68
IPV6_PEERDNS=yes
IPV6_PEERROUTES=yes
IPV6_PRIVACY=no

```
生效 `nmcli connection up enp0s3`

重启network `/etc/init.d/netword  stop/start`

如果是虚拟机选择网桥模式
