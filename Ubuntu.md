本项目选择了一台阿里云Ubuntu 16.04服务器 
### LNMP

1.更新依赖

`sudo apt-get update`

2.安装Nginx(1.10.3)

`sudo apt-get install nginx`

3.安装php-fpm(7.0.32)

`sudo apt-get install php7.0-fpm`

4.安装mysql服务端(5.7.24)

`sudo apt-get install mysql-server`

5.安装phpmyadmin

`sudo apt-get install phpmyadmin`

阿里云console会提示有sql注入

6.配置Nginx支持PHP

`sudo vi /etc/nginx/site-enable/default`

修改默认配置文件，如需多站点端口配置,复制default到同级目录
```
root /var/www/html;     修改项目根目录
index index.php index.html index.htm index.nginx-debian.html;       添加index.php默认首页
try_files $uri $uri/ =404;      Url美化，Yii2： try_files $uri $uri/ /index.php$is_args$args;
location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
}       Nginx支持php核心
```
7.测试配置文件

`sudo nginx -t`

8.重启配置生效

`sudo service nginx restart(重新启动) || sudo nginx -s reload(重新加载)`

9.开启扩展

`sudo apt-get install php7.0-curl  开启curl扩展，其他扩展同理 `

10.Nginx优化详见Nginx文档，PHP优化详见PHP文档,Mysql优化详见Mysql文档。