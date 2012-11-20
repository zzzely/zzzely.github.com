---
layout: post
title: 去除迅雷的广告、提示
comments: true
categories: [Tools&Apps]
tags: [迅雷, 广告]
---
{% include JB/setup %}
网上有很多迅雷去广告的版本，或者补丁，大家可以选择的下载，但是个人觉得总不那么靠谱，于是乎在网上搜索找到了一些方法
###去广告条  
 1. 打开迅雷的安装目录。`C:Program FilesThunder NetworkThunderProgram`（这个是默认的地址，如果安装时更改过，就按照安装的路径来找）  
 2. 找到`gui.cfg`文件，然后用记事本打开,去掉`ADServer=`和`HomePage=`两个项后的网址。或者是直接把这个文件的内容清空。  
 3. 修改完后保存。属性改为只读。
 4. 删除thunderprogram下Ad文件夹的内容。不要全部删，全部删的话一片空白太难看。`002.gif,main.gif,new.gif,default_main.swf,default_new.swf`这5个文件保留，其余的删掉。  

###去热门推荐
（这个可能不同的版本有所区别，我在5.8.14里就没有找到这个文件，能够找到的同学可以对好入座尝试下~~）  

 1. 打开迅雷的安装目录。 
 2. 找到Profiles下的`UserConfig.ini`文件，然后打开；
 3. 找到\[Splitter_1\]项下面的Pane1_Hide，将其值改为1（原始值为0）
 4. 修改完后保存。

###去搜索栏  
删除Components里的search目录。 

###去娱乐提示
删除Components里的Tips文件夹。  

另外还有会员皮肤的使用，找到迅雷按章目录下的skins 文件夹 如`C:Program Files/Thunder Network/ThunderSkins`  这里边的每一个文件夹对应着你选择使用的每个皮肤，皮肤文件夹里都有个.ini的文件，使用记事本打开  有一行关于vip的代码，其值等于1的那个，把它删掉，然后保存关闭，然后重启下迅雷，在查看-皮肤的选项里就能选择这个皮肤了。
