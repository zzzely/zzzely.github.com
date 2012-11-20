---
layout: post
title: XP下Virtualbox虚拟Ubuntu（未完） 
comments: true
categories: [OS]
tags: [windows, ubuntu, virtualbox]
---

{% include JB/setup %}
环境：主机操作系统是Windows XP，虚拟机是Ubuntu 9.10，虚拟机是VirtualBox 2.1.0。

####安装增强功能包(Guest Additions)

安装好Ubuntu 9.10后，运行Ubuntu并登录。然后在VirtualBox的菜单里选择”设备(Devices)” -> “安装增强功能包(Install Guest Additions)”。

你会发现在Ubuntu桌面上多出一个光盘图标，这张光盘默认被自动加载到了文件夹/media/cdom0。进入命令行终端，输入：

	cd /media/cdom0
	sudo ./VboxLinuxAdditions.run

开始安装工具包。安装完毕后会提示要重启Ubuntu。

####设置共享文件夹

重启完成后点击”设备(Devices)” -> 共享文件夹(Shared Folders)菜单，添加一个共享文件夹，选项固定和临时是指该文件夹是否是持久的。
共享名可以任取一个自己喜欢的，比如”gongxiang”，尽量使用英文名称。

####挂载共享文件夹

重新进入虚拟Ubuntu，在命令行终端下输入：

	sudo mkdir /mnt/shared
	sudo mount -t vboxsf gongxiang /mnt/shared

其中”gongxiang”是之前创建的共享文件夹的名字。

OK，现在Ubuntu和主机可以互传文件了。

假如您不想每一次都手动挂载，可以在/etc/fstab中添加一项

`gongxiang /mnt/shared vboxsf rw,gid=100,uid=1000,auto 0 0`

这样就能够自动挂载了。

卸载的话使用下面的命令：

	sudo umount -f /mnt/shared

**注意：**

共享文件夹的名称千万不要和挂载点的名称相同。
比如，上面的挂载点是/mnt/shared，如果共享文件夹的名字也是shared的话，在挂载的时候就会出现如下的错误信息 :

`/sbin/mount.vboxsf: mounting failed with the error: Protocol error`

具体见[传送门](http://www.virtualbox.org/ticket/2265)
