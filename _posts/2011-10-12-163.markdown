---
layout: post
title: !binary |-
  SmF2YVNjcmlwdCDmlbDnu4Tljrvph40=
wordpress_id: 163
wordpress_url: !binary |-
  aHR0cDovL3JheWNuLm5ldC8/cD0xNjM=
date: 2011-10-12 12:45:39.000000000 +08:00
---
去除数组中重复的元素是一个很常见的问题，实现起来也很简单。

原理：利用js对象（json）不会存在一样的键值key，重复的key将会被覆盖。

[javascript]
var  o = {
   x:1,
   x:2,
   x:3,
   y:4,
   'y':5
};
console.log(o);//Object { x=3, y=5}
[/javascript]

知道了这个特性就很简单了，先把Array塞进Object，再取出到Array。

[javascript]
Array.prototype.unique = function() {
	var o = {},
		arr = [];
	for(var i = 0; i &lt; this.length; i++) {
		o[this[i]] = this[i];
		console.log(this[i]);
	}
	for(var item in o) {
		arr.push(item);
	}
	return arr;
}
var a = [1,2,3,1,1,1,1,2,2,2,3,3,4,5,6,7,8,76,5];
console.log(a.unique());
[/javascript]
