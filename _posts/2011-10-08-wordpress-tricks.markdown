---
layout: post
title: !binary |-
  V29yZFByZXNzIOmaj+acuuaXpeW/lyDmnIDmlrDml6Xlv5c=
wordpress_id: 80
wordpress_url: !binary |-
  aHR0cDovL3JheWNuLm5ldC8/cD04MA==
date: 2011-10-08 08:49:27.000000000 +08:00
---
我最初调用随机日志是用的wordpress中文工具箱这个插件，这个插件用查询数据库的方式来获取随机日志，但是会出现显示不出来的问题。

在<a href="http://codex.wordpress.org/User:Environnement-France/fr:get_posts">wordpress doc</a>发现wordpress自带有个函数能实现这个功能。

[php]

&lt;?php get_posts('arguments'); ?&gt;

[/php]
[php]

//最新日志代码
&lt;?php $rand_post = get_posts('numberposts=5');
     foreach( $rand_post as $post ) : ?&gt;
     &lt;li&gt;&lt;a href=&quot;&lt;?php the_permalink(); ?&gt;&quot; title=&quot;&lt;?php the_title(); ?&gt;&quot;&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/li&gt;
&lt;?php endforeach; ?&gt;

//随机日志代码
&lt;?php $rand_post = get_posts('numberposts=5&amp;orderby=rand');
	foreach( $rand_post as $post ) : ?&gt;
	&lt;li&gt;&lt;a href=&quot;&lt;?php the_permalink(); ?&gt;&quot; title=&quot;&lt;?php the_title(); ?&gt;&quot;&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/li&gt;
&lt;?php endforeach; ?&gt;

[/php]
