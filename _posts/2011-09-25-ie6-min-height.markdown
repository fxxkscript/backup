---
layout: post
title: !binary |-
  aWU2IOWunueOsOacgOWwj+mrmOW6piBtaW4taGVpZ2h0
wordpress_id: 5
wordpress_url: !binary |-
  aHR0cDovL3JheWNuLm5ldC8/cD01
date: 2011-09-25 10:35:43.000000000 +08:00
category: css
---
先了解，IE6的<strong>!important bug</strong>

<blockquote>在IE6里，重复的属性写在同一对大括号里，后面的将会覆盖前面的，不管上面的属性是否加有!important声明；而写在不同的大括号里，它则会去认加有!important声明的那条属性。</blockquote>

其实，IE6里的height就是min-height,然后呢，利用!important优先级，实现之。看下面代码把
{% highlight css %}
.min-height {
    min-height:100px;
    height:auto !important;
    height:100px;//除了IE6之外，都会忽略这行代码
}
{% highlight %}
<code><a title="min-height" href="http://raycn.net/demo/css/min-height.html">Demo</a> </code>
