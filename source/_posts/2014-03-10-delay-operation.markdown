---
layout: post
title: "延迟操作"
date: 2014-03-10 11:15:00 +0800
comments: true
categories: [Object-C ,Study]
---
- performSelector
	- 主线程执行，否则无效
	- 非阻塞的执行方法
	- 不能取消执行
	
```objc
[self performSelector:@selector(showNextMessage)
                   withObject:nil
                   afterDelay:kMinimumMessageVisibleTime];
```

- NSTimer 定时器
	- 主线程执行，否则无效
	- 非阻塞执行方法
	- invalidate 可取消执行 	

```objc
 self.cancelSubscriotionTimer = [NSTimer scheduledTimerWithTimeInterval:3
                                                                 target:self
                                                               selector:@selector(backIsSubcribe)
                                                               userInfo:nil
                                                                repeats:NO];
                                                                
 /** 取消 */
  if ([self.cancelSubscriotionTimer isValid]) {
        [self.cancelSubscriotionTimer invalidate];
        self.cancelSubscriotionTimer = nil;
    }
```

<!--more-->

- GCD方式
	- 非阻塞执行方法
	- github上有取消执行的方法，待测试
	
``` objc
dispatch_time_t time = dispatch_time(DISPATCH_TIME_NOW, 0.3 * NSEC_PER_SEC);
                dispatch_after(time,dispatch_get_main_queue(), ^(void){
                    self.subscribeBlock(self);
                    [self.activityView stopAnimating];
                    self.subscriptionButton.userInteractionEnabled = YES;
                });
```