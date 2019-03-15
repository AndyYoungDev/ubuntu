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

