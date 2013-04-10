---
layout: post
title: Vim 支持 nesC 语法高亮
comments: true
categories: [Coding]
tags: [nesc, TinyOS, vim, syntax, highlight]
---
{% include JB/setup %}
先到这里[下载](http://bit.ly/vI8fj7)vim的nesC语法高亮插件, 最新的只有2007年的2.0版本

然后到家文件夹下 `cd ～` 新建 .vim 文件夹

`mkdir .vim` 

然后将刚刚下载vim.tar.gz解压到`.vim`文件夹下

接下来是新建.vimrc，注意是在家目录下，不是在.vim中 

`touch .vimrc`

然后将下面的内容复制到文件中
{% highlight c %}
"NesC syntax highlighting for Vim.

augroup filetypedetect
au! BufRead,BufNewFile *nc setfiletype nc
augroup END

{% endhighlight %}
然后，然后vim 就支持 nesC的语法高亮了
参考[这里](http://bit.ly/sb9Bby)
