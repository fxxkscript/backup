---
layout: post
title: !binary |-
  5paH5qGjKGRvY3VtZW50KeWSjOWFg+e0oChFbGVtZW50KeeahOWHoOS9leWF
  s+ezu+S7peWPiua7muWKqCA=
wordpress_id: 126
wordpress_url: !binary |-
  aHR0cDovL3JheWNuLm5ldC8/cD0xMjY=
date: 2011-10-10 04:56:33.000000000 +08:00
---
<h2>文档和元素的几何关系以及滚动（Document and Element Geometry and Scrolling）</h2>
<blockquote>这部分的内容是我最容易搞晕的，翻译了下权威指南第六版的相关内容。基本的内容就不说明了，例如文档坐标和视口坐标的区别。</blockquote>
一、获取滚动条位置以及视口的大小

参考：<a title="视口大小" href="http://raycn.net/122" target="_blank">http://raycn.net/122</a>

<!--more-->

二、查询元素的几何坐标

查询一个元素的大小以及位置的最方便的方法是调用它的<em>getBoundingClientRect()</em> ，这个方法最早是在IE5引入进来，现在已经被所有浏览器实现。

这个方法<strong>没有参数</strong>，返回一个<strong>对象</strong>，带有<strong><em>left,right,top,bottom</em></strong>几个属性。这几个属性其实是相对与视口的坐标。<strong>包含了border和padding，但不包含margin。</strong>（其实就是从border开始计算到视口原点的坐标）

[javascript]
var e = document.getElementById('SOME ID');
var o = e.getBoundingClientRect();
console.log(o.left);
console.log(o.top);
[/javascript]

很简单吧，你可以在firebug的控制台里试试看。

视口坐标搞定了，那轮到文档坐标啦。这时候就要利用滚动条位置来计算文档坐标咯，在前面已经写了一个计算滚动条位置的函数<em>getScrollOffset()。</em>

[javascript]
var e = document.getElementById('SOME ID');
var o = e.getBoundingClientRect();
var offset = getScrollOffset();
var x = o.left + offset.x;
var y = o.top  + offset.y;
[/javascript]

此外，在很多浏览器下<em>getBoundingClientRect()</em>，还有两个属性，<em>width和height，</em>代表元素的大小。但是IE下没有这两个属性。但是可以用right减掉left么，就是width了。height同理。见下面的代码。

[javascript]
var e = document.getElementById('SOME ID');
var o = e.getBoundingClientRect();
var width = o.width || (o.right - o.left);
var height = o.height || (o.bottom - o.top);
[/javascript]

如果元素是一个块级元素，那么没什么问题，万一是一个内联(inline)元素呢？

先看看getBoundingClientRect()的字面意思,Bounding的意思是边界，Client指的是视口，Rect意味着矩形。

注意了，如果内联元素，发生了换行，返回的坐标是什么？

举个例子：一个span元素，太长了，一行放不下，后面的内容挤到了第二行上。可以想像成span变成了一个块级元素，占据了多行，返回的值也是按照这个整体的矩形计算。

真的很难表述的清楚，有个图就简单明了了，改天弄个图上来。

那如果需要查询单行的位置呢？还有一个方法<em><strong> getClientRects()</strong></em>（注意有个s），这个方法返回的是<strong>只读</strong>的<strong>类似数组（Array-like</strong>）的对象。属性和getBoundingClientRect()类似。

最后，这两个方法是“死”的，不像DOM方法，例如getElementsByTagName()返回的是“活”（live）的对象，只要文档有所改变，就立马体现在返回的对象上。

而这两个方法，是元素位置的“快照”吧，当用户移动了滚动条，原来的对象的值不会改变。

这其实很好理解，滚动操作很频繁，如果实时更新位置，势必很影响性能。而DOM操作用户一般是不能直接操作的，都是由我们这些苦比的民工干的活。

三、滚动Scrolling

如第一部分的代码所述，scrollLeft和scrollTop是滚动条位置的属性，你可以设置这两个属性的值，从而使滚动条移动，注意那个pageXOffset是不能使滚动条移动的。

不过有些麻烦。但是可以用scrollTo()来完成这个滚动的功能，相对的坐标是文档坐标哦。还有一个方法是scrollBy()，是相对移动。这两个都是window对象下的方法。

还有一个scrollIntoView(),在相应的元素（node）下调用这个方法，可以使浏览器锚点到这个元素。和浏览器#hash锚点到&lt;a href="" name="" id=""&gt;&lt;/a&gt;是差不多的效果。

[javascript]
window.scrollTo(0,100);
window.scrollBy(0,10);
[/javascript]

学了这么多，写了个变速回到顶部的小东东。

[javascript]
function getScrollOffset(w) {
	w = w || window;
	//for all modern browsers except IE version 8 and before
	if(w.pageXOffset) {
		return {x:w.pageXOffset,y:w.pageYOffset};
	}

	//for IE in standards mode
	var d = w.document;
	if(document.compatMode == &quot;CSS1Compat&quot;) {
		return {x:d.documentElement.scrollLeft,y:d.documentElement.scrollTop};
	}
	//for browsers in Quirks mode
	return {x:d.body.scrollLeft,y:d.body.scrollLeft};
}
function goTop() {
	var x = getScrollOffset().x;
	var y = getScrollOffset().y;

	if(x&gt;0 || y&gt;0) {
		window.scrollTo(x/1.2,y/1.2);
		window.setTimeout(goTop,1);
	}
}
[/javascript]

<strong>四、更多关于元素大小、位置、overflow的内容</strong>

元素的大小：任何HTML元素都有offsetWidth、offsetHeight [只读] 两个属性，返回的是元素的宽/高，单位是CSS px。包括了元素的border和padding，但是不包括margin。

元素的位置：任何HTML元素都有offsetLeft、offsetTop属性，返回元素的x、y坐标。对于大部分元素，这些值是文档坐标；而对于已经定位的子元素、表格元素等等某些元素来说，返回的是相对与父元素的位置，有个offsetParent属性是指相对的父元素，就需要循环来计算元素的文档坐标。

[javascript]
function getElementPosition(e) {
    var x = 0 ,y = 0;
    while(e != null) {
        x += e.offsetLeft;
        y += e.offsetTop;
        e = e.offsetParent;
    }
    return {x:x,y:y};
}
[/javascript]

上面这个函数并不能精确的计算元素的文档坐标，接下来会进一步分析。

除了上面几个属性，其实所有的HTML元素都有以下一些属性。
<table>
<tbody>
<tr>
<td>offsetWidth</td>
<td>clientWidth</td>
<td>scrollWidth</td>
</tr>
<tr>
<td>offsetHeight</td>
<td>clientHeight</td>
<td>scrollHeight</td>
</tr>
<tr>
<td>offsetLeft</td>
<td>clientLeft</td>
<td>scrollLeft</td>
</tr>
<tr>
<td>offsetTop</td>
<td>clientTop</td>
<td>scrollTop</td>
</tr>
<tr>
<td>offsetParent</td>
<td></td>
<td></td>
</tr>
</tbody>
</table>
clientWidth和clientHeight，【width+padding】与offsetWidth和offsetHeight相似，但是不包括border，仅仅是padding。<strong>注意：</strong>内联元素的clientWidth和clientHeight总是为0；<strong>若有滚动条，返回值为width+padding-滚动条宽度</strong>
<ul>
	<li>clientWidth和clientHeight用在getViewportSize()中，当在文档的跟元素调用的这两个属性得到的值（在怪癖模式下，应在body上调用这两个属性）和window.innerWidth、window.innerHeight一样。</li>
</ul>
clientTop和clientLeft【border】不怎么用<strong>。</strong>一般来说指是border的宽度，<strong>但是</strong>当在上方和左方有滚动条的时候，就会包含滚动条的宽度。<strong>注意：</strong>对于内联元素是总是0。

scrollWidth scrollHeight【width + padding + overflow】是一个元素的内容区+padding+overflow的部分。如果一个区域没有overflow，那这两个的值和clientWidth和clientHeight是一样的。如果有overflow，那肯定比clienWidth和clientHeight要大。

最后，scrollTop scrollLeft是一个元素的滚动条的位置。任何元素都有这两个属性，并且是<strong>可写</strong>的。<strong>注意：</strong>HTML 元素没有scrollTo()这个方法，只有window对象有。

上面那个计算元素坐标的函数不是很精确。当元素overflow，出现滚动条时候，就需要减去滚动条的位置才是实际的位置啦。

[javascript]
function getElementPosition(ele) {
    var x = 0 ,y = 0;
    //循环，取得元素的位置。
    for(var e = ele;e != null;e.offsetParent) {
        x += e.offsetLeft;
        y += e.offsetTop;
    }
    //循环，减去祖先元素的滚动条位置
    for(e = elt.parentNode; e != null &amp;&amp; e.nodeType === 1; e = e.parentNode) {
        x -= e.scrollLeft;
        y -= e.scrollTop;
    }
    return {x:x,y:y};
}
[/javascript]

不过，一般不用getElementPosition()，因为性能底下。在现代的浏览器下直接用原生的方法getBoundingClientRect()比较好，对于老的浏览器一般有一些私有的方法，可以用jQuery等框架来做比较好。
