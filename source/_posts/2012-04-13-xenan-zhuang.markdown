---
layout: post
title: "Xen安装"
date: 2010-11-03 16:11
comments: true
categories: Study
---
<blockquote>Xen 是一个开放源代码的para-virtualizing虚拟机（VMM）。</blockquote>
基于Xen的操作系统，有多个层，最底层和最高特权层是 Xen程序本身。Xen 可以管理多个客户操作系统，每个操作系统都能在一个安全的虚拟机中实现。在Xen的术语中，Domain由Xen控制，以高效的利用CPU的物理资源。每个客户操作系统可以管理它自身的应用。这种管理包括每个程序在规定时间内的响应到执行，是通过Xen调度到虚拟机中实现。当Xen启动运行后，第一个虚拟的操作系统，就是Xen本身，我们通过xm list，会发现有一个Domain 0的虚拟机。Domain 0 是其它虚拟主机的管理者和控制者，Domain 0 可以构建其它的更多的Domain ，并管理虚拟设备。它还能执行管理任务，比如虚拟机的体眠、唤醒和迁移其它虚拟机。一个被称为xend的服务器进程通过domain 0来管理系统，Xend 负责管理众多的虚拟主机，并且提供进入这些系统的控制台。命令经一个命令行的工具通过一个HTTP的接口被传送到xend。<!--more-->

Xen的安装按照自己的操作系统的情况来选择一种安装方式。

<!--more-->

我是通过安装Opensuse操作系统来完成Xen的安装的，这中方式比较简单，只要在安装操作系统的时候，选择安装Xen就可以了。相当的傻瓜式安装。
<p style="text-align: center;"><img class="size-full wp-image-184  aligncenter" title="1" src="http://pic.mosquitoliu.com/wp-content/uploads/2010/11/1.jpg" alt="" width="496" height="375" /></p>
<a href="http://pic.mosquitoliu.com/wp-content/uploads/2010/11/1.jpg"></a>
<p style="text-align: center;"><img class="size-full wp-image-185  aligncenter" title="2" src="http://pic.mosquitoliu.com/wp-content/uploads/2010/11/2.jpg" alt="" width="500" height="375" /></p>
<p style="text-align: center;"><img class="size-full wp-image-187  aligncenter" title="3" src="http://pic.mosquitoliu.com/wp-content/uploads/2010/11/3.jpg" alt="" width="498" height="375" /></p>
&nbsp;

在这里需要注意点击软件然后选择Xen

然后一路向下

安装好后，启动系统，点击Yast2，这是需要输入密码。

选择虚拟器工具安装，安装后，重启计算机，在启动项里就可以看到Xen-Opensuse，选择此选项。进入系统后通过Yast2安装虚拟机

在安装的过程中注意，我是用镜像安装的windows server2008，选择安装全新的系统，按照提示就可以了。