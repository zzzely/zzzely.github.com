---
layout: post
title: Windows 串口接收TelosB数据
date: 2012-05-31 19:25
comments: true
categories: [Coding]
tags: [TinyOS, nesc, 串口]
---
{% include JB/setup %}

Tinyos的开发环境是基于Linux的，在Windows下也是用cygwin模拟的环境。之前在Linux下使用的用来接收串口消息的java程序无法在Windows直接编译运行，会提示关于tos-install-jni的错误。
由于有整合的需要，要在Windows下收发串口，其实需求很简单就是把之前在printfclient看到的打印消息提取出来。别的办法没有想到，就按照数据包的格式分析了十六进制的raw 数据。

如果你用串口调试助手的话应该是可以看到

	7E 45 00 FF FF 00 00 1C 00 64 53 75 62 53 65 6E 64 20 6D 65 73 73 61 67 65 20 66 72 6F 6D 20 42 20 74 6F 20 44 20 C5 4A 7E 7E 45 00 FF FF 00 00 1C 00 64 69 73 20 61 63 6B 65 64 0A 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 27 B1 7E

这样以7E开头的数据的。
如果看到的是乱码，在波特率设置都正确的情况下还是乱码的话，那可能是没有勾选上“HEX显示”这个选项。
参考[TinyOS 2.x 串口通信摘要](http://bit.ly/KLiXym)所讲的，这些数据是包含了链路层包头的数据，想要提取的消息在其中的载荷中。
现在选取其中的一段数据，以7E开头并且以7E结尾，这是一个完整的数据包。
包中各个部分的含义大概为

	7E 45 00		//同步位
	FF FF 00 00             //目的地址 FF FF（占两个Byte），源地址00 00 （占两个Byte）
	1C 			//载荷不分数据的长度 0x1C 也就是28 个Byte
	00 			//组ID
	64 			//消息类型 也就是在某些节点程序的头文件中设置的ActiveMessageType
	53 75 62 53 65 6E 64 20 6D 65 73 73 61 67 65
	20 66 72 6F 6D 20 42 20 74 6F 20 44 20
				//长度为28 的数据部分
	C5 4A 			//CRC校验的结果
	7E 			//同步</pre>

所以接收程序就可以按照数据包的格式来读取长度为28的数据。
