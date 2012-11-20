---
layout: post
title: Ubuntu 10.04 安装 TinyOS
date: 2011-12-01 10:54
comments: true
categories: [OS]
tags: [TinyOS, ubuntu]
---
这一周折腾TinyOS的环境快愁死我了，之前在windows用cygwin模拟环境安装TinyOS就遇到很多问题，但感觉还算顺利，遇到的问题都能够找到答案。

后来因为看到[这篇博客](http://bit.ly/sdLjxw)，想要使用Eclipse加上nesC的插件整一个IDE，来调试程序，但是在gdb-proxy这个地方卡了很久。

最后的结果是TI MSP430的编译工具不支持Cygwin下的jtag 和 gdb ，悲剧阿！！所以......得搬到Linux下。

本以为在Ubuntu用apt-get安装会很方便，谁想遇到了更多的问题。总结下最后的方法。

[第一种](http://bit.ly/tBN3h1) 我用它上边说的源安装以后会有问题，安装之后make micaz 平台是没有问题的，但是make telosb会有很多的错误，can not find port 之类的。

[第二种](http://bit.ly/sySY1P) 这个是真心让我感觉到希望的一篇博文啊，但是还不是很完美。加上约翰霍普金斯（jhu）的源以后可以看到基本上是从这个源获取的文件，而且个人感觉比斯坦福的要快一些。按照这个上边方法安装完成之后可以正常的make telosb，但是make micaz是不行的（小失望... ... ）

第二种方法里，修改.bashrc有一点没有提到。如果你在tos-check-jni的时候遇到没有定位到.jar和 CLASSPATH里没有 . 这两个warnning都可以通过在 .bashrc里添加

`export CLASSPATH=$TOSROOT/support/sdk/java/tinyos.jar:.`

来解决。

***

关于权限

与 Cygwin下不同的是，如果你直接进入 ` /opt/tinyos-2.1.1/app/Blink/ `下make 的话，会出现错误，一是权限不够，另外一个是神马神马error的忘记鸟。这两个错误，个人理解是在用 .bashrc配置环境变量的时候只是对当前用户配置，而在/opt目录下的app程序并不知道该按照什么样的规则来make ，所以如果在` /opt/tinyos-2.1.1/app/Blink `无法make的话，就复制到自己的文件目录里试试吧，应该是可以的。

我现在用的是telosb平台，所以只能暂且使用第二种方法来实现。
