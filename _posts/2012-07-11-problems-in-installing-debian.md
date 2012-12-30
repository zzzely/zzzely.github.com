---
layout: post
title: Debian 安装问题解决
comments: true
categories: OS
tags: [debian, problem, install]
---
{% include JB/setup %}
最近装了Debian Stable，使用DVD刻盘后安装，安装过程为图形及界面向导，没有遇到什么问题。但是安装完成后遇到一些问题

* [sudoer](#sudoer)
* [中文字体](#font)
* [ibus中文输入法](#input)
* [时间](#time)
* [浏览器(chrome & iceweasel)](#browser)
* [RTL8191SEvB无线网卡驱动](#driver)
* [登录管理器](#slim)
* [播放器](#media)
 
*** 
<h3 id="sudoer">sudoer</h3>

系统安装完成后，在终端sudo 会提示当前你的usename不是sudoer，需要讲你当前的username加入到sudoer：

可以先`su` 然后
编辑 `/etc/sudoers` 这个文件
添加一行
`username ALL=(ALL) ALL`	
username就是当前的用户名

***
<h3 id="font">中文字体</h3>
我安装的版本是英文，默认是不支持中文，需要增加对中文编码的支持：

打开终端后执行
`dpkg-reconfigure locales`
然后就可以看到图形界面的设置窗口，将其中的zh_CN的选中（空格来选择），之后系统的 locale，我还是选用的英文，当然也可以选择 zh_CN UTF-8.

系统内缺少中文字体，之后就是安装中文字体，推荐文泉驿
运行`aptitude search wqy`,找其中自己喜欢的安装，例如 zenhei，或者干脆

`apt-get install xfonts-intl-chinese wqy*`
重启或者重启gnome就可以看到中文字体显示正常了。

***
<h3 id="input">中文输入法</h3>
安装中文输入法，例如iBus

终端里
`apt-get install ibus`

`apt-get install ibus-pinyin ibus-pinyin-db-android `//安装拼音输入和词库

系统 ===> 首选项 ===> IBus 设置
设置快捷键和添加输入法到列表
最后重启iBus

*****
<h3 id="time">时间</h3>
系统安装完成后，发现时间不正确，与正常的时间有8小时时差：

Windows与Linux缺省看待系统硬件时间的方式是不一样的：

- Windows把系统硬件时间当作本地时间(local time)，即操作系统中显示的时间跟BIOS/EFI中显示的时间是一样的。
- Linux把硬件时间当作UTC，操作系统中显示的时间是硬件时间经过换算得来的，比如说北京时间是GMT+8，则系统中显示时间是硬件时间+8。

解决Debian下的时间和时区：

 - ~~在`/etc/default/rcS`里面修改，设置UTC=no~~ ` rcS `文件好像已经被忽略掉了; 可以用` hwclock -w --utc `来设置硬件时间为UTC
 - 安装ntpdate并执行时间同步:
 `apt-get install ntpdate`
 `ntpdate-debian`
想知道[其所以然](http://heart5.com/?p=98) ?

**让Windows把硬件时间当作UTC** 

开始->运行->CMD，打开命令行程序(Vista，Win7则要以管理员方式打开命令行程序方可有权限访问注册表)，在命令行中输入下面命令并回车： 
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1 

*****
<h3 id="browser">浏览器</h3>
Debian自带的浏览器使用很不爽，而且为了平时使用的扩展，很自然的想要安装chrome &firefox 。

Debian源中有开源的chrome--chromium（注意是chromium-browser，而不是chromium，那个好像是个游戏），但是版本很久，我试过了，无法进行正常的同步，虽然可以登录成功。其实chrome安装很简单，官网下载deb安装包直接安装就可以了，安装后会自动添加google chrome的源，方便以后更新。

如果遇到安装chrome时出现

	errors were encountered while processing: google-chrome-stable

的错误可以

	apt-get install libcurl3

在把系统从stable升级到testing之后，安装了chromium，但是它并不像chrome一样自带flash player

需要自行下载[插件](http://fpdownload.macromedia.com/get/flashplayer/pdc/11.2.202.258/install_flash_player_11_linux.x86_64.tar.gz) 然后将解压后的so文件放在 ` /usr/lib/chromium/plugins ` 下。

另外一个就是firefox，由于所有权的问题，firefox不在debian的源里，取而代之的是iceweasel，Debian自己编译的firefox版本，其实扩展都可以正常使用，一样的。和chromium同样的问题是版本太久了，不过可以到[mozilla debian](http://mozilla.debian.net/)选择你所需要的浏览器版本，生成相应的源，加入到 `/etc/apt/source.list`中就可以`apt-get`安装了，也很方便。

***
<h3 id="driver">无线网卡驱动</h3>
我的本本是联想的E40，无线网卡驱动需要自己安装。
`lspci`
查看设备，其中有一条
`Network controller: Realtek Semiconductor Co., Ltd. RTL8191SEvB Wireless LAN Controller`
这里有无线网卡的型号：RTL8191SEvB
到[Realtek官网下载驱动](http://bit.ly/PQyTVW)，选择相应的网卡型号（应该是RTL8191SE-VA2），下载之后解压，然后进入解压文件夹，进行编译

在编译之前需要安装cmake & linux headers，我没有网络，于是使用光盘安装
{% highlight ruby%}
apt-get install cmake linux-headers-'uname -r'
su
make
make install
sudo rmmod r8192se_pci && sleep 2 && sudo modprobe r8192se_pci
{% endhighlight %}
应该就可以了。但是从官网下载的驱动无法成功编译，在此找到一个[可用的驱动](http://pan.baidu.com/netdisk/singlepublic?fid=598732_872936164)。然后装个wicd进行管理，比较方便。
在安装完成后仍然无法链接无线，问题在于Network Manager ，将关于network manager的卸载掉就可以了。


<h3 id="slim">slim</h3>
重装系统之后将stable升级到了testing，之前在现有的系统上直接换源，更新后遇到了很多问题，索性直接重装，在干净的系统上升级了testing。
安装了slim作为登录管理器
slim的主题放在` /usr/share/slim/themes `中
然后在` /etc/slim.conf `中可以进行配置

<h3 id="media">播放器</h3>
**SMplayer**

首先，打开选项->首选项：选择字幕选项卡。
找到“默认字符编码”选项，在下拉框中选择“简体中文（cp936）”
再打开“字体和颜色”页卡（上边），选择“系统字体”在下拉选框中选择一种简体中文字体



---
__之后如遇到新的关于squeeze继续更新在本文中。__
