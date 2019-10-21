---
title: 小米手机免 root 去除广告以及卸载系统应用
date: 2019-09-18 11:27:35
categories:
tags:
    -
    -
    -
---
本文需在电脑上进行。

<!--more-->

## 手机打开 USB 调试
以及 USB 调试（安全模式）

## 下载 ADB 工具

[http://veger.ys168.com/](http://veger.ys168.com/)
在电脑软件这个文件夹里

解压后把三个文件，解压到 `C:\Windows\`里面

## 安装小米刷机工具（安装手机驱动）

http://bigota.d.miui.com/tools/MiFlash2018-5-28-0.zip

## 电脑打开 cmd
删除应用的 ADB 命令是：  
```
adb shell pm uninstall --user 0 应用包名
```
（MIUI 9、MIUI 10 测试删除后能正常开机使用）  
```
adb shell pm uninstall --user 0  com.miui.systemAdSolution （小米系统广告解决方案 必删）  
adb shell pm uninstall --user 0  com.miui.analytics （小米广告分析，必删）  
adb shell pm uninstall --user 0 com.xiaomi.gamecenter.sdk.service （小米游戏中心服务）  
adb shell pm uninstall --user 0 com.xiaomi.gamecenter （小米游戏中心）  
adb shell pm uninstall --user 0 com.sohu.inputmethod.sogou.xiaomi （搜狗输入法）  
adb shell pm uninstall --user 0 com.miui.player （小米音乐）  
adb shell pm uninstall --user 0 com.miui.video （小米视频）  
adb shell pm uninstall --user 0 com.miui.notes （小米便签）  
adb shell pm uninstall --user 0 com.miui.translation.youdao （有道翻译）  
adb shell pm uninstall --user 0 com.miui.translation.kingsoft （金山翻译）  
adb shell pm uninstall --user 0 com.android.email （邮件）  
adb shell pm uninstall --user 0 com.xiaomi.scanner （小米扫描）  
adb shell pm uninstall --user 0 com.miui.hybrid （混合器）  
adb shell pm uninstall --user 0 com.miui.bugreport （bug 反馈）  
adb shell pm uninstall --user 0 com.milink.service （米连服务）  
adb shell pm uninstall --user 0 com.android.browser （浏览器）  
adb shell pm uninstall --user 0 com.miui.gallery （相册）  
adb shell pm uninstall --user 0 com.miui.yellowpage （黄页）  
adb shell pm uninstall --user 0 com.xiaomi.midrop （小米快传）  
adb shell pm uninstall --user 0 com.miui.virtualsim （小米虚拟器）  
adb shell pm uninstall --user 0 com.xiaomi.payment （小米支付）  
adb shell pm uninstall --user 0 com.mipay.wallet （小米钱包）  
adb shell pm uninstall --user 0 com.android.soundrecorder （录音机）  
adb shell pm uninstall --user 0 com.miui.screenrecorder （屏幕录制）  
adb shell pm uninstall --user 0 com.android.wallpaper （壁纸）  
adb shell pm uninstall --user 0 com.miui.voiceassist （语音助手）  
adb shell pm uninstall --user 0 com.miui.fm （收音机）  
adb shell pm uninstall --user 0 com.miui.touchassistant （悬浮球）  
adb shell pm uninstall --user 0 com.android.cellbroadcastreceiver （小米广播）  
adb shell pm uninstall --user 0 com.xiaomi.mitunes （小米助手）  
adb shell pm uninstall --user 0 com.xiaomi.pass （小米卡包）  
adb shell pm uninstall --user 0 com.android.thememanager （个性主题管理）  
adb shell pm uninstall --user 0 com.android.wallpaper （动态壁纸）  
adb shell pm uninstall --user 0 com.android.wallpaper.livepicker （动态壁纸获取）  
adb shell pm uninstall --user 0 com.miui.klo.bugreport （KLO bug 反馈）
```

前面两个是 MIUI 系统支撑广告及精准化推送的应用，应第一时间删除，删除后不会出现无法开机的情况。这样 MIUI 系统的广告就会少很多——没有验证是否完全屏蔽。  


**【警告】以下系统自带应用删除后必定无法正常开机（来自网络），请避免误删：**  

```
com.miui.cloudservice （小米云服务）  
com.xiaomi.account （小米账户）  
com.miui.cloudbackup （云备份）  
com.xiaomi.market （应用市场）
```
