```shell
apt-get update
apt-get upgrade
cd /home
wget https://raw.githubusercontent.com/shi-yang/jnoj/master/docs/install.sh
#添加判题用户
sudo useradd -m -u 1536 judge
#git clone https://github.com/shi-yang/jnoj.git
自己复制备份的oj文件夹过去
cd jnoj
chmod 777 * -R
#LNMP 依赖服务安装
apt install nginx -y
apt install mysql-server mysql-client
apt install php-fpm php-mysql php-common php-gd php-zip php-mbstring php-xml
#改 OJ 配置文件数据库密码
nano config/db.php
#找到字段“bind-address = 127.0.0.1”，将其注释掉
nano etc/mysql/mysql.conf.d/mysqld.cnf
#密码在 /etc/mysql/debian.cnf
mysql -u debian-sys-maint -p
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'acmlab507';
quit;
mysql -u root -p
GRANT ALL PRIVILEGES ON *.* TO 'acmoj'@'%' IDENTIFIED BY 'acmlab507' WITH GRANT OPTION;
#创建表
mysql -u root -p
create database jnoj;
quit;
./yii install
# 数据库迁移工具，用于更新数据库的变化情况
./yii migrate
# 清空缓存文件
rm -rf runtime/*
cd judge
apt install libmysqlclient-dev libmysql++-dev
# 运行 OI 模式的判题机进程。对于 ，请使用 ./dispatcher -o
pkill -9 dispatcher
make
./dispatcher -o
cd ../polygon
pkill -9 polygon
make
./polygon
```
```shell
#创建开机自启判题服务脚本
cd /usr/bin
nano /usr/binServiceStart.sh
```

```
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

sudo mount /dev/sdb1 /home/disk1
sudo mount /dev/sdc1 /home/disk2
cd /home/judge/jnoj
cd judge
sudo pkill -9 dispatcher
make
sudo ./dispatcher -o
cd ../polygon
sudo pkill -9 polygon
make
sudo ./polygon
```

```shell
chmod +x ServiceStart.sh
cp ServiceStart.sh /etc/init.d
chmod 755 /etc/init.d/ServiceStart.sh
cd /etc/init.d
sudo update-rc.d ServiceStart.sh defaults 95
reboot
```

