---
layout: post
title: 遇到安全例外的提示----goagent 证书导入
comments: true
categories: [Tools&Apps]
tags: [firefox, goagent, CA]
---
{% include JB/setup %}
在家里电脑上用goagent，总是提示证书错误，确认安全例外，搞得偶烦躁不安，尝试了几次导入证书仍然失败。

其实是需要添加goagent作为一个证书机构。

如果你用的是firefox，那么 **选项--高级--加密--查看证书--证书机构--导入**，然后选择在local文件夹下的CA.crt导入就可以了~

