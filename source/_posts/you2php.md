---
title: 搭油管镜像
tags:
  - 虚拟主机
date: 2018-06-13 12:59:29
---

可以零成本观看油管视频，免费，但只能电脑网页看。
<!--more-->
项目：[https://github.com/You2php/you2php](https://github.com/You2php/you2php)

利用一台免费的虚拟主机来搭建私人镜像，然后在国内通过访问这台虚拟主机来观看油管的视频。

### 一  注册一台虚拟主机

[https://www.000webhost.com/free-website-sign-up](https://www.000webhost.com/free-website-sign-up)

当然得使用国外的，进去后填邮箱、密码、域名前缀就行，之后在邮箱里打开收到的邮件，确认邮箱即可。

### 二  YouTube API

[https://console.developers.google.com/](https://console.developers.google.com/)

当然得有谷歌账号才行的，进去后右上角，创建项目，然后默认，再点击刚才创建的项目，启用 API 和服务，YouTube Data API v3，启用，创建凭据，之后选下面这个

1.  1.  **您使用的是哪个 API？**

        YouTube Data API v3
    2.  **您从哪里调用 API？**

        网页服务器（例如 node.js、Tomcat）
    3.  **您要访问那些数据？**

        公开数据

再点  **我需要哪些凭据？**

此时就会出现API秘钥，复制保存好，然后点完成。

### 三  安装

可以去开发者的GitHub下载 [https://github.com/You2php/you2php/archive/v1.2.zip](https://github.com/You2php/you2php/archive/v1.2.zip)

也可以在我这本地下载 [download id=&#8221;240&#8243;]
<p>下载后是一个zip压缩包，解压后上传到刚才创建的虚拟主机里面。

在账号登录的情况下，打开[https://files.000webhost.com/](https://files.000webhost.com/)

应该可以进入上传文件界面吧，然后把压缩包里的所有文件都拖到 **public_html **这个文件夹里面去就行。这时候打开虚拟主机分配给你的域名，就可以来配置参数。

### 四  配置参数

都是中文，还是挺容易理解的。到最后填入之前的 **API秘钥** ，再填入邮箱就完成了。

### 最后

此时就可以通过这个 虚拟主机分配给你的域名 例如：123.000webhostapp.com 这样来观看油管的视频，可以搜索，可以下载。还是挺不错的。

