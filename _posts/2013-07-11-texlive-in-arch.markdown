---
title: 蛋疼的TeXLive
layout: post
comment: true
tags:
  - software
  - Arch
  - LaTeX
---
好久没在Arch里编译tex，Windows里后来装的那些包Arch里都没有，本来想一劳永逸地解决自动/半自动安装缺失package的问题，结果白白浪费了一上午的时间……自带的`tlmgr`没法用，aur里的`texlive-localmanager`也是千疮百孔，作者一年前就没有再维护了，参考[Arch的Wiki](https://wiki.archlinux.org/index.php/TeX_Live#TeXLive_Local_Manager)改了一下，可惜只能用一部分功能。

全手动安装一个包之后实在受不了，最后决定放大招，把Windows上MiKTeX的tex文件夹拷过来，放在`~/texmf`下面，然后`texhash ~/texmf`，终于通过了编译。MiKTeX自带的包放在`%ProgramFiles%\MiKTeX 2.9\tex`下面，编译过程中自动安装的缺失包放在`%AppData%\MiKTeX\2.9\tex`下面，都复制过去就行了。

其实想起来这个功能也不难实现，本地维护一个表，保存cls文件到对应package的映射，CTAN上的路径都是固定的，要自动下载也很简单，不知道为啥到现在都还没实现，等有时间了来试一下。
