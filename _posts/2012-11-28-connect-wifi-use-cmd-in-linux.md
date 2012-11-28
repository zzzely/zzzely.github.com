---
layout: post
title: "在Linux中使用命令行设置wpa无线连接"
description: ""
category: [OS]
tags: [linux,wpa,wifi]
---
{% include JB/setup %}
之前一直在用wicd管理无线网络，但是因为测aircrack-ng，稀里糊涂卸载掉了，顺便用了下命令行连接无线。

首先打开wlan0接口

	sudo ifconfig wlan0 up

扫描范围内的无线网络

	sudo iwlist wlan0 scan

对于采用wpa加密方式的连接，需要使用` wpasupplicant ` ,生成配置文件

	wpa_passphrase ESSID PASSWD > NAME.conf

将NAME.conf放到任意的位置，例如 ` ~/.networkconf/ ` 下

然后使用该文件连接无线网络

	sudo wpa_supplicant -B -i wlan0 -Dwext -c ~/.networkconf/NAME.conf

设置DHCP

	sudo dhclient wlan0

OK了！

