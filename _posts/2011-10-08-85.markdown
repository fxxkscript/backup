---
layout: post
title: !binary |-
  SUU2Lzcg5rWu5Yqo5YWD57Sg5o2i6KGMIGJ1Zw==
wordpress_id: 85
wordpress_url: !binary |-
  aHR0cDovL3JheWNuLm5ldC8/cD04NQ==
date: 2011-10-08 09:10:41.000000000 +08:00
---
比如有代码如下：

[html]
&lt;h1&gt;标题&lt;span&gt;更多&lt;/span&gt;&lt;/h1&gt;
[/html]

如果需要“标题”居左，“更多”居右显示在同一行，这不是很简单么，只要让span浮动到右边就是了么。

[css]
span {
    float:right;
}
[/css]

结果，你悲剧的发现，“更多”跑到了下一行去了。

so，how to fix it？

1.让span放到最前面。优点是：不用写代码。缺点：可能会破坏语义。

2.绝对定位。优点：不破坏语义。缺点：代码量加大。

3.都添加浮动。

4.添加hack。如*margin-top:XXXXpx; // 强烈不建议用hack！关于hack可以看看<a title="CSS hack" href="http://raycn.net/38">CSS hack</a>
