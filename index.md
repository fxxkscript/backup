---
layout: page
title: RayCN
tagline: Geek Inside

---
{% include JB/setup %}

这里是Ray的博客。刚刚从wordpress迁移过来！
<ul>
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

