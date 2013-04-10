---
layout: post
title: 安装VS2010 的MSDN
date: 2011-05-17 13:50
comments: true
categories: [Tools&Apps]
tags: [vs2010, msdn]
---
有些人可能会出现这样的情况，最开始安装vs的时候没有安装msdn，等到后来想要在本地查看的时候，打算重新安装却又不知从何下手。
其实很简单的：

1. 安装完VS2010后，在开始菜单中打开`Microsoft Visual Studio 2010 - Visual Studio Tools – Manage Help Settings`，第一次打开时会让你选择一个路径用于保存MSDN Library的内容，建议选择一个剩余空间比较大的盘        
2. 点击`Choose online or local help`，然后选`I want to use local help`
3. 点击`Install content from disk`，然后选择VS2010安装光盘下的`ProductDocumentationHelpContentSetup.msha`文件         
4. 点击`Add`选择你要安装的MSDN Library内容，然后点OK就开始安装了
5. 安装完成后，在VS2010里按F1即可通过默认浏览器打开Help Library，也就是传说中的msdn了。
