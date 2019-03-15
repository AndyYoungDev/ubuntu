# Ubuntu 16.04 PHP-FPM并发优化
# 流程

1.修改php工作数量,修改后性能显著提升。

`sudo vi /etc/php/7.0/fpm/pool.d/www.conf`

```
pm = dynamic
pm.max_children = 5
pm.start_servers = 2    min_spare_servers + (max_spare_servers - min_spare_servers) / 2
pm.min_spare_servers = 1
pm.max_spare_servers = 3
```

2.保存配置重启生效

`sudo service php7.0-fpm restart`