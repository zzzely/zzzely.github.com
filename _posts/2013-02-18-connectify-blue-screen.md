---
layout: post
title: "Connectify 蓝屏"
description: ""
category: OS 
tags: [connectify]
---
{% include JB/setup %}

在家里没有无线路由器只能靠笔记本为手机和pad搭建热点，但是好久不用connectify后居然遇到了问题---蓝屏

由于事先没有驱动备份，在重装系统后，就使用驱动人生更新了全部驱动

其中无线网卡驱动升级到 `Intel Wi-Fi Link 1000, 13.4.0.9`

考虑到可能是驱动兼容性的问题，于是找到Intel最新的驱动版本 `Intel_PROSet_WiFi_Win7_13.5.0` 正常使用若干分钟之后，还是跪了……

无奈之下到设备管理器中将无线网卡以及驱动删除。刷新设备后，系统会自动为无线网卡安装驱动，版本号为13.0。

世界安静了~

其实在connectify[官方support](http://support.connectify.me/entries/20316736-is-my-wi-fi-card-supported)有说明 

__Intel Wi-Fi Link 1000, 13.3.0.24   compatible __
 

