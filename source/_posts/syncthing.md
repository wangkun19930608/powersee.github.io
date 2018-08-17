---
title: 搭建个人网盘——syncthing
categories:
  - 服务器
date: 2018-05-29 23:23:19
tags: 服务器
---

### 一  下载

到其官网下载对应的客户端<!--more-->：[官网链接](https://syncthing.net/)  例如我下载Android版和Ubuntu版 Ubuntu版链接：[点我](https://apt.syncthing.net/)
安卓安装就不用说了，Ubuntu则根据其页面的这段命令输入就行。
```
\# Add the release PGP keys:
curl -s https://syncthing.net/release-key.txt | sudo apt-key add -

\# Add the "stable" channel to your APT sources:
echo "deb https://apt.syncthing.net/ syncthing stable" | sudo tee /etc/apt/sources.list.d/syncthing.list

\# Update and install syncthing:
sudo apt-get update
sudo apt-get install syncthing
```
### 二  运行

此时在Ubuntu终端输入命令：`syncthing` 来运行它 等待看到
`GUI and API listening on 127.0.0.1:8384`
同时按`ctrl 和 C` 来取消命令 运行此命令的目的时为了生成配文件

### 三  修改

此时我们即可修改配文件
`vim ~/.config/syncthing/config.xml`
然后找到 `127.0.0.1:8384` 将之改为 `0.0.0.0:8384`
更改方法为找到此处 按键盘的 `i` 便可以修改，改完按 `Esc` 退出编辑状态，输入 `:wq` (保存并退出的意思)

### 四  配置

这时就可以输入`IP:8384` (例如 `192.168.123.184:8384` )进入管理页面了 我们可以设置账号密码，以免随便他人登录这个界面 点击右上角的 操作 显示ID 将会出现一张二维码，用手机扫描这即可添加关联 然后设置想要同步的文件夹，当两个客户端都运行时就会自动同步

完
