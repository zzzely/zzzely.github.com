---
layout: post
title: windows编译安装openssl
date: 2011-04-24 13:21
comments: true
categories: [OS]
tags: [openssl, windows]
---
本文记录在Windows xp vc++6.0环境下编译安装openssl

###准备工作：

1. vc++6.0
2. 安装perl，可下载ActivePerl或者 strawberryperl安装,本次安装的是ActivePerl
3. 下载openssl 并解压，目前最新版本为1.0 此次安装为openssl-0.9.8k

###安装步骤

1. 运行cmd（or win+R）进入到vc++6.0安装目录下，运行VCVARS32.BAT 
` C:Program Files/Microsoft Visual Studio/VC98/Bin>VCVARS32.BAT ` 

2. cmd到openssl安装目录下,运行configure： ` perl Configure VC-WIN32 --prefix=c:/openssl `
创建Makefile文件： ` msdo_ms ` 

注意以下两种方式分别为动态库编译和静态库编译，根据编程时需要，可以两种方式都使用。

编译动态库：    ` nmake -f msntdll.mak `

编译静态库：    ` nmake -f msnt.mak `

（这个过程可能会稍稍漫长~ 如果出错会看到错误提示）

测试动态库：   ` nmake -f msntdll.mak test `     

测试静态库：   ` nmake -f msnt.mak test `

（测试成功会出现： ` passed all tests `)

安装动态库：    ` nmake -f msntdll.mak install `   

安装静态库：    ` nmake -f msnt.mak install ` （这个很快）

清除上次动态库的编译，以便重新编译：    ` nmake -f msntdll.mak clean `

清除上次静态库的编译，以便重新编译：    ` nmake -f msnt.mak clean `

最后生成的库文件：静态库文件在`out32`中，动态库文件在`out32dll`中
