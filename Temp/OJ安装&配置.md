`apt-get remove dnsmasq --purge && apt-get autoremove --purge && apt-get clean`


```shell
sudo apt-get update
#sudo apt-get upgrade
cd /home
wget https://raw.githubusercontent.com/shi-yang/jnoj/master/docs/install.sh
#添加判题用户
sudo useradd -m -u 1536 judge
#git clone https://github.com/shi-yang/jnoj.git
自己复制备份的oj文件夹过去
cd jnoj
chmod 777 * -R
#LNMP 依赖服务安装
sudo apt install nginx -y
#wsl必须
#nano /etc/nginx/nginx.conf
#在 nginx.conf 的 http 节点添加：
#fastcgi_buffering off;
sudo apt install mysql-server mysql-client
#找到字段“bind-address = 127.0.0.1”，将其注释掉
nano /etc/mysql/mysql.conf.d/mysqld.cnf
service mysql restart
#密码在 /etc/mysql/debian.cnf
mysql -u debian-sys-maint -p
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'acmlab507';
quit;
mysql -u root -p
GRANT ALL PRIVILEGES ON *.* TO 'acmoj'@'%' IDENTIFIED BY 'acmlab507' WITH GRANT OPTION;
quit;
service mysql restart
sudo apt install php-fpm php-mysql php-common php-gd php-zip php-mbstring php-xml
sudo apt install libmysqlclient-dev
sudo apt install libmysql++-dev
sudo apt install git
sudo apt install make
sudo apt install gcc
sudo apt install g++
sudo apt install openjdk-11-jdk
sudo bash install.sh
# 数据库迁移工具，用于更新数据库的变化情况
./yii migrate
# 清空缓存文件
sudo rm -rf runtime/*
```
```shell
#创建开机自启判题服务脚本
#cd /usr/bin
#nano /usr/bin/ServiceStart.sh
cd /etc/init.d
nano /etc/init.d/ServiceStart.sh
```

```bash
#!/bin/sh
### BEGIN INIT INFO
# Provides:          land.sh
# Required-start:    $local_fs $remote_fs $network $syslog
# Required-Stop:     $local_fs $remote_fs $network $syslog
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: starts the svnd.sh daemon
# Description:       starts svnd.sh using start-stop-daemon
### END INIT INFO

#服务启动
service ssh start
service vsftpd start
service mysql start
service php7.2-fpm start
service nginx start
#f硬盘挂载
sudo umount /dev/sdb1 /home/disk1
sudo umount /dev/sdc1 /home/disk2
sudo umount /dev/sdd1 /home/disk3
sudo mount /dev/sdb1 /home/disk1
sudo mount /dev/sdc1 /home/disk2
sudo mount /dev/sdd1 /home/disk3
cd /home/judge/jnoj
cd judge
# 运行 OI 模式的判题机进程，请使用 sudo ./dispatcher -o
sudo pkill -9 dispatcher
make
sudo ./dispatcher -o
cd ../polygon
sudo pkill -9 polygon
make
```

```shell
#chmod +x ServiceStart.sh
#cp ServiceStart.sh /etc/init.d
chmod 755 /etc/init.d/ServiceStart.sh
cd /etc/init.d
sudo update-rc.d ServiceStart.sh defaults 95
reboot
```

 