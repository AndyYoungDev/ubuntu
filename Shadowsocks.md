# Ubuntu 16.04 Shadowsocks

# 安装

1.安装pip

`sudo apt-get install python-pip`

2.安装依赖

`sudo apt-get install python-gevent python-pip python-m2crypto python-wheel python-setuptools`

3.pip安装shadowsocks

`sudo pip install shadowsocks`

4.启动shadowsocks服务

`sudo ssserver -p 8388 -k password -m rc4-md5 -d start`

-p 端口
-k 密码
-m 加密方式

