---
title: 在mac把系统固件写入U盘
categories:
      mac
date: 2018-06-01 19:03:08
---

苹果官方文章:[如何创建可引导的 macOS 安装器](https://support.apple.com/zh-cn/HT201372)

<!--more-->

最终我执行的是这一段命令

```
sudo /Volumes/Install\ macOS\ High\ Sierra/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/installMacOS --applicationpath /Volumes/Install\ macOS\ High\ Sierra/Install\ macOS\ High\ Sierra.app --nointeraction
```

分析：`（以下内容是在双击固件，将其挂载，在桌面看得到其快捷方式下进行的）`

一，这一段为固件的位置（前面到.app这一段可以通过双击打开桌面的固件，然后将里面的安装程序拖进来，而来得到地址）

```
/Volumes/Install\macOS\High\Sierra/Install\macOS\High\Sierra.app/Contents/Resources/createinstallmedia
```

二，这一段为写入的地址，即此时我命名为 installMacOS 的U盘

> /Volumes/installMacOS

三，这又为固件地址

> /Volumes/Install\ macOS\ High\ Sierra/Install\ macOS\ High\ Sierra.app

写入完成后会出现 done ，估计十几分钟，耐心等待即可。
