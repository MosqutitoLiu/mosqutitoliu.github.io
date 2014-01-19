---
layout: post
title: "腾讯微博iOS SDK使用说明"
date: 2012-04-20 18:09
comments: true
categories: [iOS ,腾讯微博iOS SDK]
---

腾序微博开放平台提供了两个iOS的SDK，一个是官方的，一个是第三方提供的。

按照官方的SDK的使用说明操作后，运行程序会报错。在程序中应该将AppDelegate.m的后缀名改成.mm。这样在模拟器中就可以运行。当真机调试的时候，需要加入CoreTelephony.framework。