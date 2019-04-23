# Ubuntu 16.04 Mysql安装及优化

# 流程
1.apt安装mysql
```bash
apt-get install mysql-server
```
2.mysql max_connections 214解决办法
* MySQL 能够支持的最大连接数量受限于操作系统,连接数与文件打开数有关.
```bash
vim /usr/lib/systemd/system/mysqld.service
```
文件末尾追加
```bash
LimitNOFILE=65535
LimitNPROC=65535
```
3.重启服务
```bash
systemctl daemon-reload
systemctl restart  mysqld.service
```
4.验证
```bash
show variables like "max_connections";
```



