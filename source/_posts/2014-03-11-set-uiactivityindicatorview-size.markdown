---
layout: post
title: "设置菊花（UIActivityIndicatorView）大小"
date: 2014-03-11 18:37:10 +0800
comments: true
categories: [Object-C ,Study]
---

```objc
_activityView = [[UIActivityIndicatorView alloc] initWithActivityIndicatorStyle:UIActivityIndicatorViewStyleWhite];
		  /** 设置中心 */
        _activityView.center = CGPointMake(30, 12);
		  /** 设置菊花大小 */
        [_activityView.layer setValue:[NSNumber numberWithFloat:0.6f]
                           forKeyPath:@"transform.scale"];
        /** 当旋转结束时隐藏 */
        [_activityView setHidesWhenStopped:YES];
        _activityView.userInteractionEnabled = NO;
        _activityView.hidden = YES;
        [_subscriptionButton addSubview:_activityView];
```