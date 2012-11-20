---
layout: post
title: TinyOS无线通信BlinktoRadio实现
date: 2011-11-18 14:12
comments: true
categories: [Coding]
tags: [TinyOS, nesc, BlinktoRadio]
---
{% include JB/setup %}
妈的早上开会因为没有实现节点间的无线通信把老师惹怒了，搞的我亚历山大。其实就是因为这个BlinktoRadio没有调出来，用的是官方下载的[BlinkToRadio](http://www.tinyos.net/tinyos-2.x/apps/tutorials/BlinkToRadio/)，平台是telosB，但是下载之后就是没有反应。
中午刚刚被告知是节点有两个不好用，容易出问题（靠~泪奔），但实际上真正的问题在于这里：

`$ cd /opt/tinyos-2.x/tos/chips/cc1000/CC1000Const.h`

这个文件中射频的频率不正确

原文件为 `#define CC1K_DEF_PRESET (CC1K_434_845_MHZ)`
修改后为 `#define CC1K_DEF_PRESET (CC1K_915_998_MHZ)`

好了，更改之后就ok了，能看到两个节点都在不停的闪啊闪的。

非常感谢[lcy1986222](http://hi.baidu.com/lcy1986222/blog/item/c4b3ec82c1db223066096e3d.html)！
