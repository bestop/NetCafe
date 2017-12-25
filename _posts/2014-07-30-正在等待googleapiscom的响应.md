---
layout: post
published: true
title: 正在等待Googleapis.com的响应
tags: 信息||Info    
permalink: /2014-07-30-正在等待googleapiscom的响应.md
---
  如果你最近在访问WordPress或其它blog的时候，遇到正在等待ajax.googleapis.com的响应，或等待fonts.googleapis.com的响应；发生网页一片空白，加载很慢的情况，说明该博客正在调用Google的JS托管或字体库，因为某种众所周知的原因，该服务目前处于失效状态。
解决方案，替换相应代码为国内的CDN公共库，即可让网站访问速度提升。   <br/>
这里360提供了一个较为简便的修改方法，只需替换一个域名就可以继续使用Google提供的前端公共库或字体库。   <br/>
1、首先在程序源代码中找到调用Google前端公共库的地址，比如：   <br/>
  `` <script type='text/javascript' src='http://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js?ver=3.4.2'></script> ``
    
    
2、将Google前端库的域名 ajax.googleapis.com 修改为：ajax.useso.com 即可，如下所示：   <br/>
  `` <script type='text/javascript' src='http://ajax.useso.com/ajax/libs/jquery/1.7.2/jquery.min.js?ver=3.4.2'></script> ``
    
    
3、自动将Google前端公共库的JS资源缓存在360网站卫士全国的CDN节点上。Have fun !
   
   
更多信息详见360常用前端公共库CDN服务平台   <br/>
 [http://libs.useso.com/](http://libs.useso.com/)   <br/>
当然，你也可以选择国内其它CDN服务：   <br/>
[http://lib.sinaapp.com/](http://lib.sinaapp.com/)   <br/>
[http://developer.baidu.com/wiki/index.php?title=docs/cplat/libs/](http://developer.baidu.com/wiki/index.php?title=docs/cplat/libs/)   <br/>
[http://www.staticfile.org/](http://www.staticfile.org/)   <br/>
[http://jscdn.upai.com/](http://jscdn.upai.com/)   <br/>
赶快试试，让你的网站访问瞬间提速吧！    
P.S: www.google.com/jsapi = ajax.useso.com/jsapi
