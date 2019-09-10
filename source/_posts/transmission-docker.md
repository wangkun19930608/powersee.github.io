---
title: BT挂机利器 transmission docker 安装法
date: 2019-09-07 22:11:40
categories:
tags:
    -
    -
    -
---
本文主要介绍如何在服务器上安装 docker，并安装 transmission 来下载 BT 种子任务。并且取回本地。

<!--more-->

> 要想进行下面的操作，需要有一个服务器，如果你没有的话， [点此链接注册充值 10 美元送 50 美元](https://www.vultr.com/?ref=8161953-4F)
> 送的 50美元只有一个月的有效期。（所以不要省，开贵点的机器吧）

上次已经用 docker 安装了 qbittorrent，这是一个非常强大的 BT 软件，我个人是非常喜欢的。但是，它占的内存比较大，如果服务器还要做一些其它的工作，用这个可能就不太合适了。

![qb speed](https://i.loli.net/2019/09/10/lJAEmdBpbHKe4u5.png)

于是， transmission 是一个不错的选择。它对硬件的配置要求非常的低，甚至在路由器上面都可以运行。

> 这次使用一台纯净系统的服务器来装。

### 安装 docker
```
curl -sSL https://get.docker.com/ | sh
```

### 安装 transmission
```
docker run -d \
--restart=always \
--name transmission \
-v /home/tr/torrents:/to_download \
-v /home/tr/download:/output \
-p 9091:9091 \
-p 51413:51413 \
-e USERNAME=admin \
-e PASSWORD=admin \
jaymoulin/transmission
```
### 解释
输入 IP:9091 即可进入 transmission 的管理界面
下载后的文件是保存在 `/home/tr/download` 这个路径下的

想要取回本地，可以和上一篇文章一样，安装 caddy ，或者也可以使用 FTP 的方法。

### 取回本地

但是下载好后文件是在服务器里，我想把它取回到电脑或者手机。那么，开启一个 http 服务即可。

这里安装一个 caddy
```
    wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/caddy_install.sh && chmod +x caddy_install.sh && bash caddy_install.sh
```
写入配置
```
echo ":80 {  
 root /home/tr
 timeouts none  
 gzip  
 browse  
}" > /usr/local/caddy/Caddyfile
```
启动 caddy
```
    /etc/init.d/caddy start
```
开放服务器 80 端口
```
ufw allow 80
```
完成后就可以在浏览器里，输入 `IP地址` 来访问下载好的文件了。如果是 MP4 文件的话，还可以支持在线播放。
