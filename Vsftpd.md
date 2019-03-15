# Ubuntu 16.04 vsftp
# 流程
1.安装vsftpd
```bash
sudo apt-get install vsftpd
```
2.添加ftp用户
```bash
sudo useradd -d /ftp目录 -s /bin/bash 用户名
```
3.给FTP用户设定密码
```bash
sudo passwd cftp
```
4.修改配置文件
```bash
write_enable=YES
chroot_local_user=YES
chroot_list_enable=YES
```
5.添加允许不锁定目录用户的文件
```bash
vi /etc/vsftpd.chroot_list
```
6.重新启动vsftpd
```bash
service vsftpd restart
```
# 注意
根目录不能有写入权限
