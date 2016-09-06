##在Ubuntu下安装Oracle Java
```
sudo rm /var/lib/dpkg/info/oracle-java7-installer* 
sudo apt-get purge oracle-java7-installer* 
sudo rm /etc/apt/sources.list.d/*java* 
sudo apt-get update 
sudo add-apt-repository ppa:webupd8team/java 
sudo apt-get update 
sudo apt-get install oracle-java7-installer
```
