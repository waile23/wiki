#su与sudo、su - root的区别

##su 和 sudo 的区别：

1. 共同点：都是root用户的权限；

2. 不同点：su仅仅取得root权限，工作环境不变，还是在切换之前用户的工作环境；sudo是完全取得root的权限和root的工作环境。


## su - root 和 su root（su）有什么区别？

`su - root`:表示人以root身份登录

just like login as root, then the shell is login shell, which mean it will expericene a login process, usually .bash_profile and .bashrc will be sourced.

`su root`:表示与root建立一个链接，通过root执行命令

like you open an interactive shell in root name.

最直接的区别就是`su`目录还是原先用户的目录

但是`su`或`su - root`后目录就变为`root`用户的主目录了。
