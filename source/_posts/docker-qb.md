---
title: 用服务器来离线下载 BT 种子，体验千兆网络的魅力——docker 安装 qBittorrent，以及把文件取回手机
date: 2019-08-29 09:54:24
categories:
tags:
    -
    -
    -
---
**此教程并不难，只要你会复制粘贴即可。**

<!--more-->

> 要想进行下面的操作，需要有一个服务器，如果你没有的话， [点此链接注册充值 10 美元送 50 美元](https://www.vultr.com/?ref=8161953-4F)
> 送的 50美元只有一个月的有效期。（所以不要省，开贵点的机器吧）

## 开始

> 使用这家的服务器，是因为它可以随时的删除，不像其它的，一买就得一年。而且，这家还可以选择自动安装 docker ，又节省了一些时间。

 1. 点击左边的 billing
 2. 充值方式支持 **支付宝** **微信**（但最少 10 美元）
 3. 充值好后 ，点右边那个 **+** 的圆圈
 4. 然后选择服务器的**地区**（日本和新加坡会比较快，不过有可能连接不上，选美国也可以）
 5.  **Server Type**点 **application** ，里面就有 **docker**
 6.  **Server Size** 就是服务器的配置，越高就越贵。（如果有赠送的 50 美元，那就选那个 40 美元的吧，反正你不花，下个月也没了）
 7. 把下面的 **Enable IPv6** 前面的 框 打钩✅（可以使我们下载时连接到更多的用户）
 8. 然后点击右下角的 deploy now
 9. 等待几分钟……
 10.就可以看到服务器部署好了，给了一个 ip 地址。


 ## 安装
 我们要控制这台服务器，需要用 ssh 工具，这里我用 putty 来演示。

> 如果用安卓手机的话，可以下载个 **JuiceSSH**

有能力的可以去 GitHub 下载：[地址](https://github.com/larryli/PuTTY/releases)
无法在 GitHub 下载的，可以到我的网盘里下载：[地址（在『电脑软件』里）](http://veger.ys168.com/)

下载后解压，打开 putty
![putty 连接.png](https://i.loli.net/2019/08/29/QwXt5dyAIofNHMW.png)
填上 IP 地址连接

接着输入用户名和密码。（密码输入时不会显示的）

连接后输入
```
    docker pull linuxserver/qbittorrent
```
完成后输入

```
docker create \
  --name=qbittorrent \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Aisa/Shanghai \
  -e UMASK_SET=022 \
  -e WEBUI_PORT=8080 \
  -p 8999:8999 \
  -p 8999:8999/udp \
  -p 8080:8080 \
  -v /path/to/appdata/config:/config \
  -v /path/to/downloads:/downloads \
  --restart unless-stopped \
  linuxserver/qbittorrent
```
创建好后再启动
```
docker start qbittorrent
```
完成后就可以在浏览器里，输入 `IP:8080` 来访问 qB 了。

## 取回本地

但是下载好后文件是在服务器里，我想把它取回到电脑或者手机。那么，开启一个 http 服务即可。

这里安装一个 caddy
```
    wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/caddy_install.sh && chmod +x caddy_install.sh && bash caddy_install.sh
```
写入配置
```
echo ":80 {  
 root /path/to/downloads
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

### 补充：

看到有些人评论说用服务器下载会有风险，这个我也是知道的。因为国外的版权保护比较严格，所以有时会监控到你在下载 BT ，如果发现你下载的内容是盗版视频之类的，有可能会对你发出警告⚠️！

但是，我说过我已经用了一年了，没有碰到过，所以才敢出这个教程。我认为可能和上传有关吧，不用上传太多应该就不太容易被查水表吧。所以我的分享率就设置为 2 而已。

> 就算你真的被警告了，一般也就是叫你把视频删了而已。如果再严重点，我大不了就把这台服务器删了，然后重新开一台。（就跟我们在网吧里一样，这也是用 vultr 的好处。）

而且，有的人问这个流量的问题，想视频中演示的，最便宜的套餐都有 1000G 流量，而且是上传 1000G，下载也 1000G ，一般使用根本是用不完的，只要设置一下这个分享率，一般是不会用超过的。

![bandi.png](https://i.loli.net/2019/08/30/tVnbi6zFp8SIED4.png)
像我这一个月才用 200G ……

暂时这些……
