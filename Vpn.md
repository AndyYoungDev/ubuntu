Vpn配置
### Vpn

1.安装pptpd

`sudo apt-get install pptpd`

2.配置Vpn账号密码

`sudo vi /etc/ppp/chap-secrets`

`echo 1 > /proc/sys/net/ipv4/ip_forward`

3.配置子网

`sudo vi /etc/pptpd.conf`

```
localip 192.168.2.1
remoteip 192.168.2.10-100
```

4.配置Google Dns

`sudo vi /etc/ppp/pptpd-options`

5.iptables配置
```
iptables -I INPUT -p tcp --dport 22 -j ACCEPT
iptables -I INPUT -p tcp --dport 1723 -j ACCEPT
iptables -I INPUT  --protocol 47 -j ACCEPT
iptables -t nat -A POSTROUTING -s 192.168.2.0/24 -d 0.0.0.0/0 -o eth0 -j MASQUERADE
iptables -I FORWARD -s 192.168.2.0/24 -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j TCPMSS --set-mss 1356
```
