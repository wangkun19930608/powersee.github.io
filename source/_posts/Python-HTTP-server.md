---
title: 用Python创建HTTP服务
tags:
  - 服务器
categories:
  - 服务器
date: 2018-05-27 16:50:38
---

一般的Linux都带有python
<!--more-->
通过命令进入所要共享的文件夹

输入这个命令
```python
python -m SimpleHTTPServer 80
```
后面的80为端口，这种适合没有搭建其它web服务的

若已经有搭建类似nginx的服务 可以通过修改端口数字，例如改为88

或者不输入端口，则会默认采用8000端口

此时输入 <span style="color: #000000;">**IP:8000**</span> 或者 <span style="color: #ff0000;">**<span style="color: #000000;">域名:8000</span>**

</span>

即可访问当前目录下的文件，如果有 **index.html **则会默认加载。

然后想要停止时，按` CTRL + C ` 取消。

* * *

**之前一直搜索想要达到这种效果，却没有找到，没想到今天偶然就看到了，哈哈**
