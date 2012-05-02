---
layout: post
title: !binary |-
  RW1hY3MgMjQg5YWl6Zeo5oyH5Y2X
wordpress_id: 213
wordpress_url: !binary |-
  aHR0cDovL3JheWNuLm5ldC8/cD0yMTM=
date: 2011-11-25 11:44:32.000000000 +08:00
---
<h2>前言</h2>
上个月，我写了篇文章<a href="http://batsov.com/articles/2011/08/19/a-peek-at-emacs24/">《Emacs 24 令人着迷的新特性》</a>。虽然Emacs 24 正式版预计在2012年春季发布，不过这并不妨碍我们现在开始使用它。你要记住的就是2011年7月，Emacs的开发团队已经完成了这一版本中所有的功能。

最近几个月，我一直在用Emacs 24，没有发现什么大的bug。唯一的障碍就是获取Emacs 24 并不是那么的容易。

接下来，我将会介绍如何再OSX、GNU/Linux和Windows下安装Emacs 24并安装一些初始化配置.

<!--more-->
<h2>安装 Emacs 24</h2>
<h4>OS X</h4>
OSX下获取Emacs 24是非常简单的。最流行有2种方法。第一种就是去<a href="http://emacsformacosx.com/">Emacs for OSX</a>下载一个pretest（或者是nightly build）最新版本的Emacs 24。我的建议是去下载最新版的pretest。

非常简单，不是么？

第二种便捷的方法是通过<a href="http://mxcl.github.com/homebrew/">homebrew</a>。在Terminal.app中，输入以下代码

[shell]
$ brew install emacs --cocoa --use-git-head --HEAD
$ cp -r /usr/local/Cellar/emacs/HEAD/Emacs.app /Applications/
[/shell]

第二步是可选的，但是推荐你这么做，应为如果你想从launchpad或者Spotlight中启动Emacs。我自己比较喜欢以daemon的方式启动Emacs(<code>emacs --daemon</code>)，这么做会加快启动Emacs的速度以及分享同一个Emacs Server，启动多个Emacsclient(<code>emacsclient -c/t</code>)。

可以调到本文配置的部分。
<h2>Linux</h2>
Linux无疑是安装Emacs方式最多的OS。显然，我们可以自己从<a href="https://github.com/emacsmirror/emacs">源代码</a>手工编译Emacs。不过，使用包管理工具无疑是更明智的做法，优点是你不用知道如何从源代码编译（这是一项复杂的工作），以及你可以保持更新，非常的方便，自动解决了依赖关系。

悲剧的是，很少有源包含了Emacs 24，幸亏有一些非官方的源有。

Debian/Ubuntu 用户可以参考 <a href="http://emacs.naquadah.org/">emacs-snapshot APT repo</a>。你会找到安装指导以及相关内容。

Gentoo 用户更加简单， 因为 Emacs 24 可以通过 <code>emacs-vcs</code> package in portage获得, 可以参考官方的文档 <a href="http://www.gentoo.org/proj/en/lisp/emacs/emacs.xml">Emacs on Gentoo page</a>。

最后，我找不到任何用RPM包(Fedora, SUSE, Mandriva, 等)编译好的Emacs 24。因为我是一个Debian的用户，我承认我没有仔细的搜索，但是从源代码安装也不是非常的难，而且你会学到很多知识啦～
<h4><strong>Windows</strong></h4>
有好几种方法去获得windows下的版本。最方便的是通过 <a>EmacsW32</a>, <a href="http://code.google.com/p/emacs-for-windows/">Emacs for Windows</a> 以及官方的 <a href="http://alpha.gnu.org/gnu/emacs/windows/">Emacs Windows builds</a>. 个人推荐官方的，非官方的包可能会包含一些其他的东东。

但是我几乎不用windows，所以也只能教你这么多了。个人推荐买个MAC，或者在*nux下使用Emacs。
<h2>初始化配置</h2>
安装Emacs非常简单，但是配置Emacs可不是这么简单的了。这就是我为什么创建了<a href="https://github.com/bbatsov/emacs-prelude">Emacs Prelude</a>-一个Emacs 24 的配置 （兼容OSX, Linux 和 Windows）

安装配置

[shell]
$ git clone git://github.com/bbatsov/emacs-prelude.git path/to/local/repo
$ ln -s path/to/local/repo ~/.emacs.d
[/shell]

Windows Vista/7 用户 ~(home) 目录是 C:\Users\\AppData\Roaming\
<h2>结语</h2>
最后，我已经介绍了如何安装Emacs 24以及提供了一个配置文件，那就没有什么借口不把你的编辑器换成Emacs 24啦。安装之，用之，爱上之。

------

原文：<a title="getting-started-with-emacs-24" href="http://batsov.com/articles/2011/10/09/getting-started-with-emacs-24/">getting-started-with-emacs-24</a>
