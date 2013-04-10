---
layout: post
title: "使用Jekyll Bootstrap搭建Blog"
description: ""
category: Tools&Apps
tags: [jekyll, blog]
---
{% include JB/setup %}

前段时间折腾了wordpress，租了空间买了域名，搭了Blog。但是访问速度并不是很理想，有时候在dashboard一会儿网页就无法打开了，更改设置都感觉很慢，不方便。诚然，wordpress是非常出色的Blog搭建工具，插件很多，主题也不错，但是对我来说都不太需要。虽然喜欢折腾，但是把时间放在这些内容的确不够划算。

于是发现了jekyll + github的组合

###Jekyll是什么

>Jekyll is a simple, blog aware, static site generator. It takes a template directory (representing the raw form of a website), runs it through Textile or Markdown and Liquid converters, and spits out a complete, static website suitable for serving with Apache or your favorite web server. This is also the engine behind GitHub Pages, which you can use to host your project’s page or blog right here from GitHub.

[Jekyll](https://github.com/mojombo/jekyll/wiki) 其实是一个转换引擎，可以把markdown文本根据模板转成html文件，也就是静态网站，这样这些内容可以很方便的放置在你的服务器上，GitHub Pages 也是这么个实现，所以你可以把网站内容放到GitHub上。

###安装Jekyll

GitHub上有详细的[安装说明](https://github.com/mojombo/jekyll/wiki/install)

最好通过RubyGems 安装

	gem install jekyll

还有安装Ruby 

	sudo apt-get install ruby1.9.1-dev

###Jekyll Bootstrap

[Jekyll Bootstrap](http://jekyllbootstrap.com/) 简化了使用Jekyll搭建Blog的过程，通过**官方[教程](http://jekyllbootstrap.com/#start-now)**, 填入你自己的GitHub USERNAME ，就可以生成个性化的安装命令，你可以很快搭建起自己的Blog。

###本地搭建jekyll server

通过Jekyll Bootstrap搭建之后，就可以在本地查看效果，满意之后再push到GitHub。

	$ cd USERNAME.github.com 
	$ jekyll --server

**注意USERNAME就是你自己的github ID。**

然后在浏览器访问 ` localhost:4000 ` 就可以看到网站了。

利用

	$ git add .
	$ git commit -m "Add new content"
	$ git push origin master

可以push到github，就像管理代码一样。



**我在安装配置的过程中遇到一些问题**

####中文列表异常

开始一段时间都以为是自己编写markdown格式错误，因为只有中文的列表就无法正确解析，包含英文的就解析正常，应该是编码的问题。

解决的方法是更换jekyll的解析引擎。

将jekyll默认的markdown解析引擎` maruku ` 更换为` RDiscount `

	sudo gem install rdiscount

然后在` _config.yml `中 ` pygments: true `之前加一行` markdown: rdiscount `,这样再次生成网站的时候就使用RDiscount来解析md文件了。

####个性化域名

USERNAME.github.com 其实是个挺不错的域名了，但是如果想绑定自己的域名，可以在` USERNAME.github.com `文件夹下新建一个CNAME 文件，里面的内容就是你的域名，比如USERNAME.COM

然后按照[GitHub所说](https://help.github.com/articles/setting-up-a-custom-domain-with-pages)将你的域名指向` 204.232.175.78 `这个ip，例如在GoDaddy中，添加一条@记录。这样当再次访问你的域名的时候，就会只想GitHub Pages了（可能DNS更新会需要一段时间）。

####favicon

如果想要个性化的标签页图标，也就是所说的favicon，可以将选定的favicon.ico 放在USERNAME.github.com文件夹根目录下就可以了。

[感谢](http://kyle.xlau.org/posts/github-cname.html)





