---
title: VPS离线下载文件最简易方案
date: 2018-08-04 05:48:34
tags:
categories:
  - 服务器
---
### 所使用的工具：
- Aria2
- caddy
- AriaNg
<!--more-->
脚本来自**逗比根据地**


### 首先安装 下载工具-- Aria2
```
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/aria2.sh && chmod +x aria2.sh && bash aria2.sh
```
按 1 ，就可以安装。成功后会看到这样的显示。
![image](/img/2018/Aria2-done.png)

由于我们用 ssh 登录 vps 后，默认是在 root 目录下。因此我想让下载位置也在这之下，方便以后用命令行删除文件。

因此需先创建文件夹

```
mkdir -p web/down
```
然后进入 Aria2 来需改下载位置和密码

```
./aria2.sh
```
选择 ++7. 修改 配置文件++

再选择 ++4.  修改 Aria2 密码+端口+文件下载位置++

密码就个人按喜好改了，端口就不改了，按回车键使用默认即可，下载位置就改为新的路径

```
/root/web/down
```
再次看到 ==Aria2 启动成功 !  == 这部分就完成了。


---
### 安装使用界面
下载工具安装完成了，那要怎么用它呢？难道用命令行来下载文件？虽然确实可以，不过这有点……

还是图形界面比较任性化，点点几下就行。

#### 安装 web 服务器 caddy

```
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/caddy_install.sh && chmod +x caddy_install.sh && bash caddy_install.sh
```
#### 写入配置到 Caddy 配置文件
```
echo ":80 {
 root /root/web
 timeouts none
 gzip
 browse
}" > /usr/local/caddy/Caddyfile
```

#### 下载 AriaNg
```
cd web && wget https://github.com/mayswind/AriaNg/releases/download/0.4.0/aria-ng-0.4.0.zip && unzip aria-ng-0.4.0.zip
```
这里出错的话，可能是因为没有安装 unzip 这个应用，根据提示安装下即可。

#### 启动 caddy

```
/etc/init.d/caddy start
```

---
### 下载文件并取回本地
这时候就可以用浏览器，通过 IP 或者域名来访问下载界面。需要设置一下。
![image](/img/2018/AriaNg.png)

第一个红圈可以填 IP 和域名，都行的。第二个红圈就是填刚才设置的密码了。

连接上会有左下角有绿色的已连接提醒。然后就可以下载文件了，也可以下载种子。

下载完就在我们的 vps 里面，那要怎么取回本地呢？只需要在浏览器地址栏里，在  IP 或者域名后面加上 /down 就行。例如
> 115.152.148.55/down

就会显示下载的那些文件。

---
这个方法呢，是我个人觉得比较简易的，比较适合我自己的。下载完就在命令行里用
> rm -rf web/down/*

来删除所有的文件。

因此也就不去搞那些需要 PHP 的了。也因为下载完就删除，所以也没必要设置需要密码才能访问文件列表。
