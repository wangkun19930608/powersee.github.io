---
title: 服务器搭建全能下载器 Aria2 以及私人网盘，只需一行命令（docker）
date: 2019-09-16 19:40:18
categories:
tags:
    -
    -
    -
---
本文将利用 docker 一键安装 Aria2 和 filebrowser。

<!--more-->

建议搭配之前的文章来观看：[用服务器来离线下载 BT 种子，体验千兆网络的魅力](/2019/08/docker-qb)

[项目 GitHub 地址](https://github.com/wahyd4/aria2-ariang-docker/blob/master/README.CN.md)

### 安装 docker(如果机器没有的话）

```
curl -sSL https://get.docker.com/ | sh
```

### 最快速启动
```
docker run -d --name aria2-ui -v /home/down:/data -p 80:80 wahyd4/aria2-ui
```

- Aria2: http://yourip/ui/
- FileManger: http://yourip
- 请使用 admin/admin 进行登录

这样下载的文件都放在 `/home/down` 这个文件夹里面

文件夹没有写入权限，有兴趣看这篇文章了解 [文章链接](https://note.qidong.name/2018/01/docker-volume-permission/)
不管原理，无脑给予 777

```
chmod 777 /home/down
```

强制删除容器

```
docker rm -f aria2-ui
```
### 加密下载界面
```
docker run -d --name ariang \
  -p 80:80 \
  -e PUID=1000 \
  -e PGID=1000 \
  -e ENABLE_AUTH=true \
  -e RPC_SECRET=Hello \
  -e ARIA2_SSL=false \
  -e ARIA2_USER=user \
  -e ARIA2_PWD=pwd \
  -v /home/down:/data \
  wahyd4/aria2-ui
```

- 用户名：user
- 密码：pwd

### 后续补充

根据个人的需求来选择，如果觉得不需要加密 Aria2 的管理界面的，其实用第一种方式就行了。非常简单，一行命令即可。

同时也可以结合 APP ：Transdrone_2.5.15.apk 来使用，这个我放在网盘里，使用它来管理多个下载工具也是比较方便的。

http://veger.ys168.com/

![transdrone](https://i.loli.net/2019/09/30/SZ4jLRqiB5dzNgF.png)
