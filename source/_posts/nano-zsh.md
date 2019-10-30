---
title: 小钢炮又被折腾坏记录，最终成功用上 zsh
date: 2019-10-26 19:31:39
categories:
tags:
    -
    -
    -
---


刚才给小钢炮安装了 zsh ，这个过程还是有点复杂的，不过好在都能找到教程。

<!--more-->

## 1、先去看灯大的这个文章



[https://gitee.com/8ox86/phicomm-n1-issue/wikis/entware%20guide?sort_id=1368793](https://gitee.com/8ox86/phicomm-n1-issue/wikis/entware%20guide?sort_id=1368793)



让我们可以用 opkg2 来安装其它应用



## 2、安装 zsh 与配置集



于是我就安装了 zsh 以及 oh my zsh 为的就是用这个自动补全插件 zsh-autosuggestions


```
opkg2 install zsh
```
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
```
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```


## 3、遇坑部分，无法 ssh 连接



顺利地安装成功了，然后，我想将 zsh 设置为默认的 shell ，使用 chsh -s /opt/bin/zsh 却失败了。

然后网上找其它方法，看到有个是修改 /etc/passwd 这个文件，第一行就是 root 用户的默认 shell 路径，于是用 vim 修改这个文件，改为 zsh 的路径，然后退出，再重新 ssh 连接，就登录不了了……

![](/img/2019/can't login after edit the passwd.jpg)

本想这次扑街了，又得重装系统了，可惜 qb 的配置没有备份……



## 4、想办法备份



于是想办法看看能不能备份出来，不然重装系统后所有记录都没了。想到 qb 的配置文件是放在 /var/lib/qbittorrent 这个文件夹里的，之前我是 ssh 之后，把复制到自己的硬盘的。现在无法 ssh，得另寻方法。



于是想到小钢炮的 web 界面有个定时任务的功能 Scheduled Tasks ，在这个我也可以执行命令啊，那我在这里备份这个文件夹不就行了。

同时灯大的 wiki 里也有写备份 qb 和 tr 的方法，他是用 tar 来打包这个文件夹的，这种可能更好吧。



于是我添加了这条任务，每十五分钟就将这两个文件夹打包备份到我这个叫 one 的硬盘里。


```
15 * * * * tar cvf /media/one/qb.tar /var/lib/qbittorrent && tar cvf /media/one/tr.tar /var/lib/transmission
```


## 5、曲线救国



所以这样打包好后，就可以重装系统了嘛。不过我突然想到，既然这里可以执行命令，那我在这里修改 passwd 这个文件，改回去不就行了？



于是我将 passwd 这个文件的内容，输出到硬盘里

```
cat /etc/passwd > /media/one/pass.txt
```


接着我用 filebrowser 修改这个文档里面的内容，再把它输入回 passwd

```
cat /media/one/pass.txt > /etc/passwd
```


完成，再来 ssh ，就成功登录上了。



但是我的 zsh 还是没办法设置为默认 shell ……



怎么办呢？



## 6、用上 zsh



我想到，当我们用 ssh 连接上小钢炮的 sh 时，它会去执行 /etc/prifile 这个文件里面的内容，那我直接在这里面添加一行


```
zsh
```


我将它放在环境变量之后，在 13 行这个位置。这样之后用 ssh 连接，系统就会先启动 sh ，然后读取 /etc/prifile 的内容，读到 13 行，执行了 zsh 这个命令，然后 shell 就自动切换到 zsh 了。



由于这个过程很快，我们不可能看到，所以一连接上看到的就是 zsh 了。完美！
