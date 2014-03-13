---
layout: post
title: "setNeedsLayout VS setNeedsDisplay"
date: 2014-03-12 14:38:33 +0800
comments: true
categories: [Object-C ,Study]
---
- setNeedsLayout
	- 异步执行
	- 不立即刷新布局
	- 自动调用layoutSubViews（重新定义子元素的位置和大小）
		- layoutSubViews方法优先于drawRect
		- layoutSubViews被调用的情况：
			- init初始化不会调用layoutSubViews，但是当initWithFrame进行初始化的时候，rect的值不为CGRectZero，会触发调用layoutSubViews
			- addSubView会触发layoutSubViews
			- 设置view的frame（frame的值设置前后发生了变化）会触发 layoutSubViews
			- 滚动UIScrollView触发layoutSubViews
			- 旋转Screen触发UIView上的layoutSubViews
	- layoutIfNeeded 立即刷新布局
- setNeedsDisplay
	- 异步执行
	- 重新绘制
	- 自动调用drawRect
		- drawRect被调用的情况
			- UIView初始化没有设置rect大小，导致drawRect不被调用
			- UIViewController中的loadView、viewDidLoad两方法之后调用（可以设置一些值给View） 
			- sizeToFit之后触发drawRect
			- 设置contentMode属性值为UIViewContentModeRedraw，设置或更改frame时自动调用drawRect
			- 若要用CALayer绘图，只能在drawInContext中绘制，或是在delegate中的相应的方法中绘制，同样调用setNeedsDisplay触发