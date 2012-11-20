---
layout: post
title: MFC中MessageBox的用法
date: 2010-07-15 20:41
comments: true
categories: [Coding]
tags: [mfc]
---
{% include JB/setup %}
消息框是个很常用的控件，属性比较多，本文列出了它的一些常用方法，及指出了它的一些应用场合。

1. MessageBox("这是一个最简单的消息框！");
2. MessageBox("这是一个有标题的消息框！","标题"); 
3. MessageBox("这是一个确定 取消的消息框！","标题", MB_OKCANCEL ); 
4. MessageBox("这是一个警告的消息框！","标题",MB_ICONEXCLAMATION ); 
5. MessageBox("这是一个两种属性的消息框！","标题",MB_ICONEXCLAMATION|MB_OKCANCEL );
6. if(MessageBox("一种常用的应用","标题",MB_ICONEXCLAMATION|MB_OKCANCEL)==IDCANCEL) return;

附其它常用属性

**系统默认图标，可在消息框上显示** 

- X错误 MB_ICONHAND, MB_ICONSTOP, and MB_ICONERROR 
- ?询问 MB_ICONQUESTION
- !警告 MB_ICONEXCLAMATION and MB_ICONWARNING 
- i信息 MB_ICONASTERISK and MB_ICONINFORMATION

**按钮的形式** 

- MB_OK 默认 
- MB_OKCANCEL 确定取消 
- MB_YESNO 是否 
- MB_YESNOCANCEL 是否取消
 
**返回值** 

- IDCANCEL 取消被选 
- IDNO 否被选 
- IDOK 确定被选 
- IDYES 是被选
