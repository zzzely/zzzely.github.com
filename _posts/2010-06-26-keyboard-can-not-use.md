---
layout: post
title: (键盘)代码 19：由于其配置信息（注册表中的）不完整或已损坏，Windows无法启动这个硬件设备 解决方法
comments: true
categories: [OS]
tags: [vmware, 键盘]
---

{% include JB/setup %}
今天装VMware实在是郁闷，安装过程出错，卸载又有问题，最后被我直接在注册表里删了内容，这下倒好，重启之后键盘无法使用了，触摸板也失效了。

在BIOS下试了下，不是键盘本身的问题，估计是Windows的某些硬件驱动被我误删了，在安全模式下清掉了密码。

在设备管理器中看到了键盘那一条上有个黄色的感叹号！ 详细的信息是“代码 19：由于其配置信息（注册表中的）不完整或已损坏，Windows 无法启动这个硬件设备” 还好找到一位老兄的博客，跟我遇到一样一样的问题，欣慰呀～～ 

##方法是这样的：

首先打开注册表，由于键盘失效了，不能在“运行”中敲regedit，只好找到注册表编辑器的程序。
在C:WINDOWS下，regedit.exe，就是有个立方体图标的那个。定位到`HKEY_LOCAL_MACHINESYSTEMCurrentControlSetControlClass{4D36E96B-E325-11CE-BFC1-08002BE10318}`

删除UpperFilters

卸载设备，重新启动。  

然后设备管理器里变成：代码 10：该设备无法启动。

定位到`HKEY_LOCAL_MACHINESYSTEMCurrentControlSetControlClass{4D36E96B-E325-11CE-BFC1-08002BE10318}`;  

添加字符串UpperFilters，内容是kbdclass  

**注意：这里是新建“字符串”，而不是新建“项”**

然后重启  OK了！  
