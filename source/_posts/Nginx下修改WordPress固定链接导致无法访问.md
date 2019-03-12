---
title: Nginx下修改WordPress固定链接导致无法访问
date: 2019-03-12 09:08:51
categories:
tags:
    - wordpress
    -
    - 
---
内容来自：[CSDN](https://blog.csdn.net/csdn1161851523/article/details/52942404)

<!--more-->

先找到配置文件的位置，如我这里是
```
/usr/local/nginx/conf/nginx.conf
```
用 vim 来修改，在server{}  字段   中的  “root /websit/wwwroot/;”(这行就是指定网站所在目录的)  这一行的下面 ，添加下面的内容：
```
    if (-f $request_filename/index.html){
    rewrite (.*) $1/index.html break;
    }
    if (-f $request_filename/index.php){
    rewrite (.*) $1/index.php;
    }
    if (!-f $request_filename){
    rewrite (.*) /index.php;
    }

    rewrite /wp-admin$ $scheme://$host$uri/ permanent;
```
然后重启 Nginx ，如果和我一样是用 lnmp 的，可以输入
```
lnmp nginx restart
```
之后就可以访问了文章了。
