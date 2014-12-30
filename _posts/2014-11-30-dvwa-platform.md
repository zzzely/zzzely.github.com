---
layout: post
title: "DVWA训练平台"
description: ""
category: IS
tags: [DVWA, 渗透]
---
{% include JB/setup %}


DVWA训练平台
常见WEB渗透方式的一个演练平台，可以本地搭建。LAMP环境即可。
>登录：

>user:admin

>password:password

开始对常见方法进行测试前，需要在setup中创建数据库。

在DVWA Security可以设置平台的安全层级，`low 、medium 、high `

页面中的view source 可以查看服务器端php代码，并且支持compare不同安全层级的代码查看。

渗透方式包括爆破、CSRF、SQL注入、盲注、文件上传、反射和存储型XSS等等。

学习过程中会使用到一些常用的工具，如Burp Suite、 Firefox 插件 hackbar 等。

主要参考的教程是：

[Web漏洞实战教程(DVWA的使用和漏洞分析)2013完整版](http://www.freebuf.com/articles/web/7084.html)

[DVWA WEB安全训练平台 PPT](http://pan.baidu.com/s/1c04aZZU) _密码：q7ps_

这些渗透方式的原理在《白帽子讲Web安全》中都有很详细的说明。
