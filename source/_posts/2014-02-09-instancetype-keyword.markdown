---
layout: post
title: "instancetype关键字"
date: 2014-02-09 11:14:55 +0800
comments: true
categories: [Object-C ,Study]
---
instancetype关键字，保证了编译器能够正确推断方法的返回的类型。

[Clang](http://clang.llvm.org/docs/LanguageExtensions.html#objective-c-features)的文档里提到 "instancetype is a contextual keyword that is only permitted in the result type of an Object-C method" 也就是说,instancetype只能作为返回值，不能像id那样作为参数。
