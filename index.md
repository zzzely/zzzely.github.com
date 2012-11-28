---
layout: page
title: 停摆
tagline: stop the clocks! 
---
{% include JB/setup %}

  **这是使用Jekyll Bootstrap搭建的Blog，托管在github上。 在这里折腾些杂七杂八，写些有的没的。** 
***

<ul class="posts">
  {% for post in site.posts limit:20%}
    <li><span>{{ post.date | date_to_string }}</span> &raquo;&raquo;  <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>

  {% endfor %}
</ul>

<div style="width:50%;margin-left:auto;margin-right:auto;text-align:right;c    lear:both;">
          <a href="/archive.html">查看全部{{site.posts.size}}篇文章...</a>
</div>

***

**花些时间给自己感兴趣的、有意思的东西，希望可以一直记录下去……**
