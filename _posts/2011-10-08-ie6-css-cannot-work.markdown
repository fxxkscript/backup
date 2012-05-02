---
layout: post
title: !binary |-
  SUU2IENTU+agt+W8j+mDqOWIhuWkseaViA==
wordpress_id: 88
wordpress_url: !binary |-
  aHR0cDovL3JheWNuLm5ldC8/cD04OA==
date: 2011-10-08 14:23:46.000000000 +08:00
---
满足下面条件就会引起 注释下面的样式不起作用：
1. css有中文注释
2. css为ANSI编码
3. html为utf-8编码

解决方法：
1. 去掉中文注释，用英文注释
2. 统一css 和 html 的编码

建议采用第二种解决方法

ps： css为uft-8 html 为ANSI 不会出现失效的情况。规范的编码还是非常重要的。
<h2></h2>
