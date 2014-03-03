---
layout: post
title: "UILabel设置text显示不同颜色不同字体"
date: 2014-03-03 14:43:10 +0800
comments: true
categories: [Object-C ,Study]
---
```objc

……

UILabel *countLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 10, 150, 14)];

NSString *text =[NSString stringWithFormat:@"共有%d条评论",self.datasource.total];

countLabel.attributedText = [self setCmtHeaderViewLabel:text];

……

/**
 * 设置label.text中的数字和文字的颜色
 * 数字-RGB(51, 51, 51)
 * 文字-RGB(102, 102, 102)
 */
- (NSAttributedString *)setCmtHeaderViewLabel:(NSString *)text
{
	/** 转为可变属性的字符串 */
    NSMutableAttributedString *attrText = [[[NSMutableAttributedString alloc] initWithString:text] autorelease];
    [attrText addAttribute:(NSString *)NSFontAttributeName
                     value:(id)[[UIFont systemFontOfSize:15] CTFonter]
                     range:NSMakeRange(0, text.length)];
    [attrText addAttribute:(NSString *)NSForegroundColorAttributeName
                     value:(id)RGB(102, 102, 102).CGColor
                     range:NSMakeRange(0, text.length)];
    [attrText addAttribute:(NSString *)NSForegroundColorAttributeName
                     value:(id)RGB(51, 51, 51).CGColor
                     range:NSMakeRange(2, text.length - 5)];
    return attrText;
}
```
