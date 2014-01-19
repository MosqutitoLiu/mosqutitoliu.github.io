---
layout: post
title: "Windows live writer连接wordpress"
date: 2010-11-03 15:04
comments: true
categories: 应用
---
<p style="text-align: center;"><a href="http://pic.mosquitoliu.com/wp-content/uploads/2010/11/writer-thumb.jpg"><img class="size-full wp-image-177  aligncenter" title="writer-thumb" src="http://pic.mosquitoliu.com/wp-content/uploads/2010/11/writer-thumb.jpg" alt="" width="420" height="261" /></a></p>
与插件无关

进入后台的 设置-撰写 确保下边两项打上勾，保存

<a href="http://pic.mosquitoliu.com/wp-content/uploads/2010/11/298ecc1ac426.jpg"></a>

tp登陆，到root/wp-includes,下载文件class-IXR.php，然后再本地使用相关编辑器（我用EditPlus）打开，ctrl+F查找length，然后找到：

<!--more-->

$length = strlen($xml);
变为
$length = strlen($xml)+3;

刷新，重新上传，问题解决，ok！