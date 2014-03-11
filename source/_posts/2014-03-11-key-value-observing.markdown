---
layout: post
title: "Key-Value-Observing"
date: 2014-03-11 15:59:28 +0800
comments: true
categories: [Object-C ,Study]
---
Key-Value-Observing（简称KVO）：当指定的属性被修改，允许对象接受到通知的机制。每次指定的被观察对象的属性被修改的时候，KVO都会自动的去通知相应的观察者。

- 优点
	- 当有属性改变时，KVO会提供自动的消息通知。不需要设计自己的观察者模型
	- 支持多个观察者观察同一个属性
	
- 使用
	- 是否有必要实现KVO
	- 注册成为观察者
	- 实现addObserver:forKeyPath:option:context:方法
	
		```objc
		 [self addObserver:observer
                forKeyPath:@"edit"
                   options:NSKeyValueObservingOptionNew|NSKeyValueObservingOptionOld
                   context:NULL];
        ```
        
       - self : 被观察者
       - observer ：观察者             
       - foreKeyPath ：property的name
       - NSKeyValueObservingOptionNew 更改之前的值提供给处理方法；NSKeyValueObservingOptionOld 更改之后的值提供给处理方法；NSKeyValueObservingOptionInitial 把初始化的值提供给处理方法，一旦注册就会调用一次；NSKeyValueObservingOptionPrior 分两次调用，在值改变之前和改变之后
       - context ：可以带一些参数
	- 当观察者的属性变化的时候方法observeValueForKeyPath:ofObject:change:context:会自动调用