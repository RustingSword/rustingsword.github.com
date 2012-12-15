---
layout: post
title: "用AutoHotkey让Foxit Reader模拟Vim的操作"
tags: ["software"]
---

我已经有一段时间没用过鼠标了（因为无线鼠标电池用完了懒得去买……），平时可以用小红点，但是翻文档（主要是看pdf）的时候没啥好办法。习惯了Vim的按键，再用方向键觉得很别扭，[Apvlv](http://naihe2010.github.com/apvlv/)功能还是弱了一点，那就用[AHK](http://www.autohotkey.com/)曲线救国吧。

很简单粗暴的方法：

    ;在Foxit中模拟Vim的操作
    #IfWinActive, ahk_class classFoxitReader
    j::Down
    k::Up
    h::Send ^+{Tab}
    l::Send ^{Tab}
    ^f::PgDn
    ^b::PgUp
    ~~G::End~~ ;ahk不区分大小写……
    g::Home
    o::Send ^o
    d::Send ^w
    q::Send !{F4}
    #IfWinActive

不过有时候`^f`和`^b`会失效，不知道为啥，往下翻页还能用空格来代替，往上翻页就只能用pageup了。
