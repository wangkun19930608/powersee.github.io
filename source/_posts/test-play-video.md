---
title: 测试播放视频
date: 2018-09-02 16:51:06
categories:
tags:
    - 网络
    -
    -
---
在博客上可以用嵌入的方式，引用优酷和 YouTube 的视频，那么可以播放放在网站的视频吗？
<!--more-->

下面依然用这串代码
```
<iframe height=315 width=560 src='视频的相对路径' frameborder=0 allowfullscreen></iframe>
```

在本地的启动 web 服务，然后在浏览器打开博客首页，视频可以播放。不错，手机端也可以正常访问。此时将网页和视频文件放置在 GitHub 上，同样可以播放。有点意外，除了加载比较慢，总体感觉不错。

<iframe height=315 width=560 src='/misc/1.mp4' frameborder=0 allowfullscreen></iframe>
