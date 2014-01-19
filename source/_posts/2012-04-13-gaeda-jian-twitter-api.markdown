---
layout: post
title: "GAE搭建Twitter API"
date: 2010-09-02 00:46
comments: true
categories: 应用
---
<strong>一、创建Application</strong>
<p style="text-align: left;">1.登入<a title="查看 GAE 的全部文章" href="http://immmmm.com/tag/gae" target="_blank">GAE</a>创建Application：打开<a rel="nofollow" href="https://appengine.google.com/" target="_blank">https://appengine.google.com/</a>，点击“Create an Application”，填写两个输入框内容（<strong>记下Identifier</strong>），再点击“Create Application”，提示成功，OK；<a href="http://lh3.ggpht.com/_65ZfNm-tR48/TGubP6MMG4I/AAAAAAAAD3k/6aCekuhnoKQ/gae-1.jpg?imgmax=800"><img class="pie-img aligncenter" src="http://lh3.ggpht.com/_65ZfNm-tR48/TGubP6MMG4I/AAAAAAAAD3k/6aCekuhnoKQ/gae-1.jpg?imgmax=400" alt="gae-1.jpg" /></a></p>
2.登入<a title="查看 推特 的全部文章" href="http://immmmm.com/tag/%e6%8e%a8%e7%89%b9" target="_blank">推特</a>创建application获取key及secret：打开<a rel="nofollow" href="https://twitter.com/apps" target="_blank">https://twitter.com/apps</a>（需翻墙），点击“Register a new application »”，按照下图进行填写后点击“Save”；<!--more-->

其中Callback URL是：http://xxxxxx.appspot.com/oauth/twitter/callback （xxxxxx是第一步创建时的Identifier名称）
<p style="text-align: center;"><a href="http://lh6.ggpht.com/_65ZfNm-tR48/TGubRDnyE_I/AAAAAAAAD4s/oULmlmkrAE0/gae-3.jpg?imgmax=800"><img class="pie-img aligncenter" src="http://lh6.ggpht.com/_65ZfNm-tR48/TGubRDnyE_I/AAAAAAAAD4s/oULmlmkrAE0/gae-3.jpg?imgmax=800" alt="gae-3.jpg" /></a></p>
<p style="text-align: left;">成功后出现以下页面，<strong>记下</strong><strong>key和secret</strong>，OK；</p>
<strong>二、gtap程序下载及修改</strong>

1.下载并解压<a rel="nofollow" href="http://code.google.com/p/gtap/downloads/list" target="_blank">gtap-0.4</a>；

2.修改代码并保存：

(1)app.yaml
<p style="text-align: center;"><img class="pie-img aligncenter" src="http://lh6.ggpht.com/_65ZfNm-tR48/TGubTvQw9wI/AAAAAAAAD38/OI6bTNYflg4/gae-7.jpg?imgmax=800" alt="gae-7.jpg" /></p>
<p style="text-align: left;">(2)main.py</p>
<p style="text-align: center;"><img class="pie-img aligncenter" src="http://lh3.ggpht.com/_65ZfNm-tR48/TGubUD9fvrI/AAAAAAAAD4A/7Y29bYU0ZMI/gae-8.jpg?imgmax=800" alt="gae-8.jpg" /></p>
<strong>三、本地部署配置<a title="查看 GAE 的全部文章" href="http://immmmm.com/tag/gae" target="_blank">GAE</a>并上传gtap</strong>

1.下载并安装<a rel="nofollow" href="http://www.python.org/download/" target="_blank">Python</a>和<a rel="nofollow" href="http://code.google.com/intl/zh-CN/appengine/downloads.html" target="_blank">Google App Engine SDK for Python</a>；

2.配置Python：计算机—属性—高级系统设置—环境变量，修改“系统变量”中的“Path”值为Python的安装目录
<p style="text-align: center;"><a href="http://lh6.ggpht.com/_65ZfNm-tR48/TGubSkBc-gI/AAAAAAAAD30/1ErS4ipY6qE/gae-5.jpg?imgmax=800"><img class="pie-img aligncenter" src="http://lh6.ggpht.com/_65ZfNm-tR48/TGubSkBc-gI/AAAAAAAAD30/1ErS4ipY6qE/gae-5.jpg?imgmax=400" alt="gae-5.jpg" /></a></p>
然后win+r，输入cmd回车，输入python，有返回，说明Python配置成功，OK；

3.上次gtar程序至GAE：启动Google App Engine Launcher，点击“File”，再点击“Add Existing Application”，选择指定到gtar程序所在文件夹的路径（需全英文路径），然后选中新项目，再点击主界面上的“Deploy”按钮输入 Google账户及密码，等待弹出窗口中显示“You can close this window now”，OK；

<strong>四、完成Ouath验证</strong>

访问<a href="http://xxxxxx.appspot.com/">http://xxxxxx.appspot.com/</a>，
<p style="text-align: center;"><a href="http://lh3.ggpht.com/_65ZfNm-tR48/TGubUy9YkvI/AAAAAAAAD4E/Y0w9kFbY00Q/gae-9.jpg?imgmax=800"><img class="pie-img aligncenter" src="http://lh3.ggpht.com/_65ZfNm-tR48/TGubUy9YkvI/AAAAAAAAD4E/Y0w9kFbY00Q/gae-9.jpg?imgmax=400" alt="gae-9.jpg" /></a></p>
<p style="text-align: left;">点击“Allow”：</p>
<p style="text-align: center;"><a href="http://lh5.ggpht.com/_65ZfNm-tR48/TGubVoQrhkI/AAAAAAAAD4I/uQglo_TqWsY/gae-10.jpg?imgmax=800"><img class="pie-img aligncenter" src="http://lh5.ggpht.com/_65ZfNm-tR48/TGubVoQrhkI/AAAAAAAAD4I/uQglo_TqWsY/gae-10.jpg?imgmax=400" alt="gae-10.jpg" /></a></p>
<p style="text-align: left;">页面跳转回来：</p>
<p style="text-align: center;"><a href="http://lh5.ggpht.com/_65ZfNm-tR48/TGubWF8BGlI/AAAAAAAAD4M/thiUcsZXi14/gae-11.jpg?imgmax=800"><img class="pie-img aligncenter" src="http://lh5.ggpht.com/_65ZfNm-tR48/TGubWF8BGlI/AAAAAAAAD4M/thiUcsZXi14/gae-11.jpg?imgmax=400" alt="gae-11.jpg" /></a></p>
<p style="text-align: left;">最后点击“Change the Key”，OK！（页面会跳转上个界面不用管，直接关闭就行了）</p>
<p style="text-align: left;"><strong>五、您的推特API出炉</strong>：http://xxxxxx.appspot.com/ （最后那个“/”不可省！）</p>