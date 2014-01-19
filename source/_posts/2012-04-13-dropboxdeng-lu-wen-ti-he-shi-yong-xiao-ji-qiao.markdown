---
layout: post
title: "Dropbox登陆问题和使用小技巧"
date: 2010-05-16 13:40
comments: true
categories: 应用
---
<p style="text-align: center;"><a href="http://pic.mosquitoliu.com/wp-content/uploads/2010/05/CD83392C1AD5EFF44AE03A78E54D1B2015555CF9.jpg"><img class="aligncenter size-full wp-image-170" title="CD83392C1AD5EFF44AE03A78E54D1B2015555CF9" src="http://pic.mosquitoliu.com/wp-content/uploads/2010/05/CD83392C1AD5EFF44AE03A78E54D1B2015555CF9.jpg" alt="" width="405" height="258" /></a><a href="http://pic.mosquitoliu.com/wp-content/uploads/2010/05/CD83392C1AD5EFF44AE03A78E54D1B2015555CF9.jpg"></a></p>
Dropbox作为一个强大文件网络同步、备份、分享工具深受大家的喜爱，但是被和谐掉了。Dropbox无法登陆，其解决办法如下：

在hosts文件中将dropbox对应的IP修改为174.36.30.71，hosts文件的目录一般是在C:WindowsSystem32 driversetc

<!--more-->使用Dropbox同步收藏夹

默认情况下IE的收藏夹路径为： C:Documents and SettingsAdministratorFavorites ，我们可以通过修改注册表的方式来修改收藏夹的路径，打开注册表： HKEY_USERsSoftwareMicrosoftWindowsCurrentVersionExplorerUser Shell Folders ，而后把“Favorites”键值修改成My Dropbox目录下的一个文件夹路径即可。在多台电脑都进行这样的操作，就可以实现多台电脑自动同步IE收藏夹的功能。