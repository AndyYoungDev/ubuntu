# Ubuntu 16.04 Nginx并发优化

# 流程

1.修改处理器数量

`worker_processes auto;`

2.修改事件模型

```
events {
        worker_connections 768;     单进程处理外部连接的数量
        multi_accept on;    尽可能多地处理请求
        use epoll;      Ubuntu事件模型
}
```

3.没有太大的文件上传需求建议降低时间（单位：s）

`keepalive_timeout 65;`

4.请求成功日志

`access_log off;`

生产环境关闭成功日志

5.gzip看情况调整压缩级别

`gzip_comp_level 4;`

笔者常用为4

6.测试并重启生效

`sudo nginx -t` 测试通过后 `sudo service nginx restart(重新启动) || sudo nginx -s reload(重新加载)`

7.并发查看配置

```
location /bingfa {
   stub_status on;
}
```
```bash
Active connections    #当前 Nginx 正处理的活动连接数.

server accepts handledrequests  #总共处理了*个连接,成功创建*次握手,总共处理了*个请求.

Reading         #nginx 读取到客户端的 Header 信息数.

Writing         #nginx 返回给客户端的 Header 信息数.

Waiting         #开启 keep-alive 的情况下,这个值等于active-(reading+writing),意思就是Nginx已经处理完正在等候下一次请求指令的驻留连接
```
8.命令行查看并发配置

```bash
netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a,S[a]}'
```

```bash
SYN_RECV        #一个连接请求已经到达，等待确认

ESTABLISHED     #正常数据传输状态/当前并发连接数

FIN_WAIT2       #另一边已同意释放

ITMED_WAIT          #等待所有分组死掉

CLOSING         #两边同时尝试关闭

TIME_WAIT       #另一边已初始化一个释放

LAST_ACK        #等待所有分组死掉
```
