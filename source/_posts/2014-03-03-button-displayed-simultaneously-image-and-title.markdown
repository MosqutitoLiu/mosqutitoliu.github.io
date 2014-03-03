---
layout: post
title: "UIButton-Image和Title共显"
date: 2014-03-03 16:45:22 +0800
comments: true
categories: [Object-C ,Study]
---
一般情况下设置button的setBackgroundImage，然后setTitle,这样button的image和title都能显示正常。
有时候需要设置button的setImage，在这种情况下再设置setTitle会发现没有共同显示，只是看到image看不到title。其原因是title的位置出现了错误，title的坐标是相对image的坐标。

如：image为下图所示
<iframe src="https://www.flickr.com/photos/mosquitoliu/12905710443/player/30106a7a12" height="48" width="120"  frameborder="0" allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>
添加显示title
```objc
……
UIImage *isSubscriptionImage = [UIImage imageWithNameOnly:kIsSubscriptionImageName];
    
    [self.subscriptionButton setTitle:kIsSubscriptionTitleNSString
                             forState:UIControlStateNormal];
    [self.subscriptionButton setImage:isSubscriptionImage
                             forState:UIControlStateNormal];
    [self.subscriptionButton setTitleColor:RGB(84, 185, 252)                                 
    						  forState:UIControlStateNormal];
    						  
    self.subscriptionButton.contentHorizontalAlignment = UIControlContentHorizontalAlignmentRight;
    /** 设置title的坐标 */
    [self.subscriptionButton setTitleEdgeInsets:UIEdgeInsetsMake(0, -isSubscriptionImage.size.width - 10, 0, 10)];
    ……
```
效果如下所示：
<iframe src="https://www.flickr.com/photos/mosquitoliu/12905989023/player/1d4e627ca6" height="48" width="120"  frameborder="0" allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>
