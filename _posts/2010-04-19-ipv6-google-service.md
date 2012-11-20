---
layout: post
title: ipv6使用Google服务
comments: true
categories: Tools&Apps
tags: [google, ipv6]
---
{% include JB/setup %}
今天reader的时候看到GFW Blog上的一篇牛文，关于ipv6的使用。 
众所周知，GFW的强大日益明显，实际上今天博文上说的等效于使用ipv6来翻墙。其实说翻墙并不确切，只是利用ipv6的服务器来直接定位到ip地址，
并不是使用网路上的DNS来解析，方法很简单，修改hosts文件。
对hosts有所了解的xd们应该知道这是很常用的访问被墙网站的方式，以前没听说过的呢就是自己来写URL和ip地址的对应关系。

**如何安装IPV6**

Vista和Win7默认已经安装了ipv6协议，所以无需再次安装。在XP和win2003下，

* 第一种办法：本地链接，右键属性，“安装”，选择“协议”，选择“Microsoft TCP/IP 版本 6”，确定；
* 第二种办法：手动，打开命令行窗口，`C:>ipv6 install`，回车；
* 第三种办法：安装utorrent（个人强烈建 议的BT/PT下载客户端），在选项中 点击“安装IPv6/Teredo”按钮，自动安装IPv6
 
**如何启用IPV6**

上面所言，只是安装了IPV6协议，而不是已经完成了IPV6的配置，能浏览IPV6网站了——当然，如果你是校园网用户，并且所在学校已经开通了IPV6，另当别论——对普通ADSL用户来说，目前常用的使用ipv6的办法有两个。
* 第一种：采用isatap隧道，有些学校提供了免费的isatap隧道供公众使用，甚至不需要注册，以下是最常用的四个

	isatap.tsinghua.edu.cn(清华大学的)
	isatap.shu.edu.cn(上大的) 
	isatap.hust.edu.cn(华中科大的) 
	isatap.sjtu.edu.cn(上交的)

启用：打开命令行窗口（如果是Vista/Win7用户，需要到开始菜单→附件→命令行窗口→右键以“管理员权限运行”），手动设置isatap隧道，比如添加上海交大的免费隧道：

    C:UsersAdministrator>netsh 
    netsh>int ipv6 isatap 
    netsh interface ipv6 isatap>set router isatap.sjtu.edu.cn enable

一共就输入三条命令（上文>之后的），每输入一条回车确认，
测试IPV6配置是否已成功

* 第一种方法：如上图的命令行窗口中，先输入exit退出netsh配置， 然后键入ipconfig /all，回车。在得到的结果中，查看一下有没有形如 2002:77a6:6eba::77a6:6eba 这样的东东，比如2001或2002，有的话基本确定已成功；
* 第二种方法：访问一下http://ipv6.google.com 能找到服务器的话，说明已启用ipv6；
* 第三种方法：访问一下http://www.kame.net 看看顶部的乌龟，是活动的则说明已启用IPV6，静止的则是IPV4；

我试过了命令行的安装方法，因为前两天刚刚重装了系统，还是需要安装ipv6的。
isatap隧道我按上面说的使用了上交的，设置成功之后发现[google ipv6](http://ipv6.google.com)中的Google logo可以动的哟！真的可以动哟~以前真的没有发现过。

这里是一份hosts列表，主要是Google的各项服务[点击查看](http://docs.google.com/View?id=dfkdmxnt_61d9ck9ffq)。

如果不想自己更改的话，可以从这里[下载](http://code.google.com/p/ezpctk/downloads/detail?name=hosts.rar&amp;can=2&amp;q=)
下载之后复制到C:Windows/system32/driver/etc文件夹中，替换即可。
现在，打开你的Firefox或者Chrome等浏览器，是不是可以看YouTube了？是不是也可以打开Blogger了？
哈哈，在教育网也可以这么爽啦~~

