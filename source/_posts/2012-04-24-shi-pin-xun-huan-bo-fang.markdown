---
layout: post
title: "视频循环播放"
date: 2012-04-24 17:42
comments: true
categories: [iOS ,MPMoviePlayerViewController]
---

{% codeblock %}
moviePlayer = [[MPMoviePlayerViewController alloc] initWithContentURL:url];

moviePlayer.moviePlayer.repeatMode = MPMovieRepeatModeOne;//循环播放
……
{% endcodeblock %}