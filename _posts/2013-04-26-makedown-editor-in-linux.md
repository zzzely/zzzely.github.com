---
layout: post
title: "Linux下Markdown文本编辑器"
description: ""
category: 
tags: [markdown, retext, vim]
---
{% include JB/setup %}

用jekyll写blog需要用markdown文本转为html文件发布。作为主流的文本格式，Vim当然对markdown的支持是非常好的

##Vim编辑markdown##

下载[Vim插件](http://www.vim.org/scripts/script.php?script_id=1242)，解压后会得到两个`mkd.vim`文件，分别在`syntax`和`ftdetect`文件夹下，将这两个文件复制到`~/.vim`相应的`syntax`和`ftdetect`下即可

	cp ./syntax/mkd.vim ~/.vim/syntax/
	cp ./ftdetect/mkd.vim ~/.vim/ftdetect/

但是，在vim下，中文的输入还是相对蛋疼的，不过还好，还有其他的选择。

##Retext编辑markdown##

___Retext is a simple but powerful text editor for Markdown and reStructuredText.It is written in Python using Qt libraries, able to run on any platforms.___

[Retext](http://sourceforge.net/p/retext/home/ReText/)是一个用Python实现的跨平台的支持markdown的文本编辑器。它可以支持实时的效果预览，也可以将文件输出HTML/PDF/ODT等格式。

对我来讲，如果输入中文的话，还是无模式的编辑器相对舒服些，尤其是在我没有搞定sublime text的中文输入的时候。使用时可以进行简单的设置。


* __输入中文__：不过第一次打开，还是没法成功输入中文，需要 右键 -> Select IM -> iBus
* __及时预览__：Ctrl + L
* __调整字体__：默认的显示字体较小，需要更改配置，一般在~/.config/ReText project/ReText.conf.不过需要调整的是`editorFontSize`属性，而非`fontSize`属性；

[这里](http://sourceforge.net/p/retext/wiki/Configuration%20file/)还有很多设置的说明。
