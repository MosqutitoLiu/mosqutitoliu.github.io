---
layout: post
title: "UITapGestureRecognizer屏蔽掉Button的点击事件"
date: 2014-04-07 23:39:05 +0800
comments: true
categories: [Object-C ,Study]
---
iOS 6以下UITapGestureRecognizer会屏蔽掉Button的点击事件,但是在iOS 7就不会。
解决办法：
```objc
#pragma mark - UIGestureRecognizerDelegate
- (BOOL)gestureRecognizer:(UIGestureRecognizer *)gestureRecognizer shouldReceiveTouch:(UITouch *)touch
{
	if ([touch.view isKindOfClass:[UIButton class]]) {
        /** iOS 6 以下UITapGestureRecognizer会屏蔽掉Button的点击事件 */
        return NO;
    }
    
    return YES;
}
```
