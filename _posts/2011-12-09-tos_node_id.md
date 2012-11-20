---
layout: post
title: TinyOS中的TOS_NODE_ID
comments: true
categories: [Coding]
tags: [TinyOS, nesc]
---
{% include JB/setup %}

>修改 `opt/tinyos-2.x/tos/system/tos.h` 中的`uint16_t TOS_NODE_ID = x`;
>则编译后下载到节点的TOS_NODE_ID值会发生改变

实际上，给节点设定地址并不是用这种不科学的方法的，头文件给出的是默认值，是在不指定地址的时候使用的。

`make telosb install.X`

使用上面的命令是将程序下载到TelosB节点上，而其中的“X”就是对节点给定的地址，链路层地址，如果不重新下载程序是不可以改变的。
