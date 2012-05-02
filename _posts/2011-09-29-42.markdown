---
layout: post
title: !binary |-
  SmF2YVNjcmlwdDogVGhlIERlZmluaXRpdmUgR3VpZGUg6K+75Lmm56yU6K6w
  5LmL5qC45b+D56+H
wordpress_id: 42
wordpress_url: !binary |-
  aHR0cDovL3JheWNuLm5ldC8/cD00Mg==
date: 2011-09-29 14:00:52.000000000 +08:00
---
<strong>零、前言</strong>

距离上次看JavaScript（简称JS）权威指南中文版第五版已经好久了，JS水平依然没有进步。最近迫于压力，细细品味下JS第六版的英文原版。特写下此篇博文来记录学习时遇到的问题。需要学习的同学还是应该先看看js权威指南先。

<strong> 一、JavaScript核心篇</strong>

1.JavaScript的类型：2大类，原始类型和对象类型。

原始类型包括：number,string,boolean,null,undefined.其中null和undefined是两种特殊类型。
<ul>
	<li>typeof null === Object，这表明null可以认为是一种特殊的对象的值，代表没有对象。通常，null被视为一种单独类型的单独成员，可以是numbers,strings,Object的值，意味着no value；</li>
	<li>而typeof undefined === undefined。undefined通常是声明了一个变量，但没有给变量付值，导致变量的值为undefined。</li>
</ul>
对象类型：除了上面5种原始类型，其余的都是对象类型。js里的对象是属性的集合（json）。

<strong>变量之间的转换：</strong>

最常见的就用强制类型转换，Number() String() Boolean() ,返回的是原始类型哦！

通常会遇到数字和字符串之间的转换
<ul>
	<li>Convert <strong>Number</strong> to <strong>String</strong></li>
</ul>
1)通过+号运算符

[javascript]
100 + &quot; &quot; //return &quot;100&quot;
[/javascript]

2)强制类型转换

[javascript]
String(100);//return &quot;100&quot;
[/javascript]

3)toString()方法

[javascript]
var n = 100;
n.toString();//return &quot;100&quot;
[/javascript]
<ul>
	<li>Convert <strong>String</strong> to <strong>Number</strong></li>
</ul>
1)通过 - 或者 * 运算符

[javascript]

&quot;1234&quot; - 0 //return 1234

&quot;1234&quot; * &quot;1&quot; //return 1234

[/javascript]

2)强制类型转换

[javascript]

Number(&quot;1234&quot;)

[/javascript]

3) parseInt() parseFloat()

这两个函数转换并返回字符串开头的数字，并忽略尾部的非数字字符。前者只适用于整数，后者即适用于浮点数，又适用于整数。若字符串中以"0x"或者“0X”开头，则自动转换成十六进制。以"0"开头的则表示8进制。

[javascript]

parseInt(&quot;1234abc&quot;);//return 1234

parseFloat(&quot;123.122jjj&quot;);//return 123.122

parseInt(&quot;011&quot;);//return 9

parseInt(&quot;0x11&quot;);//return 17

//这两个内置函数还可以有第二个参数，代表数的进制,范围在[2-36]之间

parseInt(&quot;11&quot;,8);//return 9

parseInt(&quot;11&quot;,32);//return 33

[/javascript]

<strong>2.Global Object全局对象</strong>

JS里有一个全局对象，这个对象在浏览器里是window。

[javascript]
this === window //return true;
[/javascript]

<!--more-->

<strong>3.Wapper Object 包装对象</strong>

[javascript]
var s = &quot;hello javascript&quot;;//一个字符串变量
var word = s.substring(s.indexOf(&quot; &quot;)+1,s.length);//s不是一个对象么，怎么还能够调用方法？其实，是把原始类型临时转换成对象类型，就好像调用了new String(s)，一旦使用完，临时对象自动销毁。
[/javascript]

再看下面的代码，来验证上面所述的理论

[javascript]
var s = &quot;hello javascript&quot;;
s.len = 10;
console.log(s.len);//输出undefined，说明了s.len只是s临时转换成了object。
[/javascript]

4.变量声明&amp;&amp;变量作用域

[javascript]
var num = 1;
console.log(num);//1
console.log(delete this.num);//false
console.log(num);//1
[/javascript]

&nbsp;

[javascript]
num = 1;
console.log(num);//1
console.log(delete this.num);//true
console.log(num);//num is not defined
[/javascript]

由此可见，变量没有声明var而直接付值，num = 1 相当于 this.num = 1，且this===Global Object,其实就是全局对象的一个属性，当你没有使用var声明变量时，变量是可以被delete删除的。当使用了var声明变量，变量是不可以被delete删除,是noconfigurable的。但还是可以用this读取到。

[javascript]
var truevar = 1;
fakevar = 2;
this.fakevar2 = 3;
console.log(this.truevar === truevar);//true
delete truevar;//false
delete fakevar;//true
delete fakevar2;//true
[/javascript]

变量作用域，js里没有block scope（C语言里块级作用域），只有function scope；

[javascript]
var scope = &quot;Global&quot;;
(function() {
    var scope = &quot;local&quot;;
    console.log(scope);//local
}());
[/javascript]

&nbsp;

[javascript]
var scope = &quot;Global&quot;;
(function() {
    scope = &quot;local&quot;;
    myscope = &quot;local&quot;;//隐式声明全局变量
}());
console.log(scope);//local
console.log(myscope);//local
[/javascript]

&nbsp;

[javascript]
var scope = &quot;gloabl&quot;;
(function() {
    var scope = &quot;local&quot;;
    (function() {
        var scope = &quot;nested&quot;;
        console.log(scope);//nested
    }());
}());
[/javascript]

看懂了么？所以，声明变量是一定要用var哦，不要觉得js是一门松散语言就掉以轻心了。

关于function scope,看一个例子你就懂了。

[javascript]
var scope = &quot;global&quot;;
function() {
    console.log(scope);//输出global?输出变量未定义错误？错了，孩子，其实是undefined，声明了，但是没有赋值；
    var scope = &quot;local&quot;;//变量在这里初始化，但是声明存在于整个function scope。
    console.log(scope); //这个呢？输出其实是lcoal
}
[/javascript]

相当于下面这个代码

[javascript]
var scope = &quot;global&quot;;
function() {
    var scope;
    console.log(scope);//undefined
    scope = &quot;local&quot;;//变量在这里初始化
    console.log(scope); //lcoal
}

[/javascript]

为什么呢？
<h2>变量声明提升（Hoisting）</h2>
JavaScript 会<strong>提升</strong>变量声明。这意味着 <code>var</code> 表达式和 <code>function</code> 声明都将会被提升到当前作用域的顶部。

在function中，不管你变量是在哪里声明，整个function scope都会声明有这个变量，只是在赋值之前，scope都是undefined，只有运行到赋值的时候，变量才会初始化；

由这个例子看出，js变量习惯上声明在function scope的顶部。

<strong>Scope Chain 变量作用域链</strong>

全局变量在一个程序中都是“可见”的，局部变量只在函数中和nested function（内部的函数）中可见。

里层的函数可以访问到外层函数声明的变量,反过来就不可以了。

for in

注意不是所有属性都可以遍历，所有自己创建的属性和方法是可以枚举的（但是，在ECMAScript5中可以使之不可枚举）

[javascript]
var o = {
    x:1,
    y:2,
    z:{
        a:10,
        b:20,
        c:{
            s:&quot;aaa&quot;,
            ss:&quot;bbb&quot;
        }
    }
};
function count(o) {
    for(var i in o) {//这里的i是一个字符串，so，不能用o.i访问属性，只能用o[i]啦。
        console.log(o[i]);//1,2,object；for in是不能遍历到更深的object啦
    }
}
count(o);
[/javascript]

如果要遍历对象中所有的属性，应该像下面这个程序所写，需要手动的遍历到更深的地方。

[javascript]
var o = {
    x:1,
    y:2,
    z:{
        a:10,
        b:20,
        c:{s:&quot;aaa&quot;,ss:&quot;bbb&quot;}
    },
};
var num = 0;
function count(o) {
    for(var i in o) {
		if(typeof o[i] === &quot;object&quot;) {
			count(o[i]);
			return;
		}
		num++;
    }
}
count(o);
console.log(num)//6
[/javascript]

Array

[javascript]
var a = [1,2,3,4,5];
delete a[1];
console.log(a);//[1,undefined,3,4,5]
[/javascript]

如果要删除一个数组元素，用delete只是把值设为undefined。

如果用for in 遍历数组，会跳过undefined这个值。

[javascript]
var a = [1,2,3,4,5];
delete a[1];
console.log(a);//[1, undefined, 3, 4, 5]
for(i in a) {
    console.log(a[i]);//1 3 4 5
}
[/javascript]

可见删除一个数组元素用delete比较麻烦了。正好，Array对象里提供了很多强大的方法供你使用。例如删除、添加、查找元素可以用splice这个强大的方法。

PS:推荐看一看JavaScript Garden，对你学习JS有很大的帮助。<a title="JavaScript Garden" href="http://bonsaiden.github.com/JavaScript-Garden/zh/">http://bonsaiden.github.com/JavaScript-Garden/zh/</a>

&nbsp;
