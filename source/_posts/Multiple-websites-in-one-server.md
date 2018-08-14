---
title: 让一个服务器拥有多个网站
tags:
  - 服务器
date: 2018-05-28 04:10:15
---
可以在一台机器上放置多个网站，若是静态网站的话，理论上可以放置无限多个。

<!--more-->

### 本操作基于Ubuntu

我的nginx访问的根目录 
```
/home/wwwroot/default
```
创建一个”vhost”目录
```
sudo mkdir /usr/local/nginx/conf/vhost
```
* * *

<span style="color: #ff0000;">创建siteA的配置文件</span>
```
sudo vi /usr/local/nginx/conf/vhost/vhost_siteA.conf
```
<pre class="lang:default decode:true">    server {
    listen       80;                        # 监听端口
    server_name www.siteA.com siteA.com;    # 站点域名
    root  /home/wwwroot/default;              # 站点根目录
    index index.html index.htm index.php;   # 默认导航页

    location / {
        # WordPress固定链接URL重写
        if (!-e $request_filename) {
            rewrite (.*) /index.php;
        }
    }

    # PHP配置
    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
    }
}</pre>

* * *

<span style="color: #ff0000;">创建siteB的配置文件</span>
```
sudo vi /etc/nginx/vhost/vhost_siteB.conf
```
<pre class="lang:default decode:true ">    server {
    listen       80;                        # 监听端口
    server_name www.siteA.com siteA.com;    # 站点域名
    root  /home/wwwroot/old;              # 站点根目录
    index index.html index.htm index.php;   # 默认导航页

    location / {
        # WordPress固定链接URL重写
        if (!-e $request_filename) {
            rewrite (.*) /index.php;
        }
    }

    # PHP配置
    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
    }
}</pre>

* * *

修改nginx.conf
```
sudo vi /usr/local/nginx/conf/nginx.conf
```
在http里加入这段
```
include /usr/local/nginx/conf/vhost/*.conf;
```

重启 nginx 即可。

