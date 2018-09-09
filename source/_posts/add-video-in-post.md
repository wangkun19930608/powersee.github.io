---
title: 文章中插入服务器的视频
date: 2018-09-02 16:51:06
categories:
tags:
    - 网络
    -
    -
---
在博客上可以用嵌入的方式，引用优酷和 YouTube 的视频，那么可以播放放在网站（服务器）的视频吗？
<!--more-->

下面依然用这串代码
```HTML
<iframe height=315 width=560 src='视频的相对路径' frameborder=0 allowfullscreen></iframe>
```

在本地的启动 web 服务，然后在浏览器打开，视频可以播放。不错，手机端也可以正常访问。此时将网页和视频文件放置在 GitHub 上，同样可以播放。但是有个缺点，一打开就自动播放，不知道怎么关闭。

后来了解到用 video 标签的话，就可以设置它不自动播放，并且如果想让视频能够自动适应大小，只需要加上 div 标签就行。如下面这样
```html
<div  width="100%">
<video height="100%" width="100%" src="视频路径" controls="controls"></video>
</div>
```

<div  width="100%">
<video height="100%" width="100%" src="/misc/1.mp4" controls="controls"></video>
</div>
