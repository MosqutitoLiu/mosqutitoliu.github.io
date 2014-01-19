---
layout: post
title: "内存管理"
date: 2012-04-16 15:58
comments: true
categories: [Study ,Object-C]
---
Objective-C使用了一种叫做持有计数（Retain Count）的机制来管理内存中的对象。
在Objective-C中每个对象都对应着他们自己的持有计数（Retain Count），持有计数可以理解为一个整数计数器，当使用alloc方法创建对象的时候，持有计数会自动设置为1。当你向一个对象发送retain消息时，持有计数数值会增加。相反，当你像一个对象发送release消息时，持有计数数值会减小。当对象的持有计数变为0的时候，对象会释放自己所占用的内存。


<!--more-->

#一、引用计数是实例对象的内存回收唯一参考

引用计数(retainCount)是Objective-C管理对象引用的唯一依据。调用实例的release方法后，此属性减一，减到为零时对象的dealloc方法被自动调用，进行内存回收操作，也就是说我们永不该手动调用对象的dealloc方法。

下面就是它主要操作接口：

1. alloc, allocWithZone,new(带初始化)

	为对象分配内存，retainCount为“1”，并返回此实例
	
2. release

	retainCount 减“1”，减到“0”时调用此对象的dealloc方法
	
3. retain

	ratianCoutn 加“1”
	
4. copy、mutableCopy

	复制一个实例，retainCount数为“1”，返回此实例。所得到的对象是与其它上下文无关的，独立的对象
	
5. autorelease

	在当前上下文的AutoreleasePool栈顶的autoreleasePool实例添加此对象，由于它的引入使Objective-C由全手动内存管理上升到半自动化。
	
#二、Object-C内存管理准则

我们可以把上面的接口按对retainCount的操作性质归为两类

Ａ类是加一操作：1，3，4
Ｂ类是减一操作：2，5（延时释放）内存管理准则如下：
1. A与Ｂ类的调用次数保持一制
2. 为了很好的保障准则一，以实例对象为单位，谁A了就谁Ｂ，没有第二者参与例：  

		
	NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
		NSObject *o = [[NSObject alloc] init];    //retainCount为1
		/[o retain];    //retainCount为2
		//[o release]; //retainCount为1
		//[o autorelease]; //retainCount为1
		[pool release]; //retaincount为0，触发dealloc方法 
	

#三、AutoreleasePool使Objective-C成为内存管理半自动化语言
程序入口
	NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
		int retVal = UIApplicationMain(argc, argv, nil, nil);
		[pool release];
	

在 声明pool后，release它之前的这段代码，所有段里的代码（先假设中间没有声明其它的AutoreleasePool实例），凡是调用了 autorelase方法的实例，都会把它的retainCount加1，并在此pool实例中添1次此实例要回收的记录以做备案。当此pool实例 dealloc时，首先会检查之前备案的所有实例，所有记录在案的实例都会依次调用它的release方法。



	NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
		NSObject *o = [[NSObject alloc] init];
		[o autorelease];                                //在pool实例dealloc时，release		一次此实例，重要的是并不是在此行去release
		NSLog(@"o retainCount:%d",[o retainCount]);    //此时还可以看到我们的o实例还是可用的，并且retainCount为1
		[pool release];    //pool 的 retainCount为0，自动调用其dealloc方法，我们之前备案的小o也将在这里release一次（因为咱们之前仅仅autorelease一次）
	
	



真对同一个实例，同一个Pool是可以多次注册备案(autorelease)的。在一些很少的情况化可能会出现这种需求：




	NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
		NSObject *o = [[NSObject alloc] init];
		[o retain];
		[o autorelease];
		[o autorelease];
		[pool release];
	




我 们调用了两次A类(retainCount加1的方法)，使其retainCount为2，而接下来的两次autorelease方法调用，使其在 pool中注册备案了两次。这里的pool将会在回收时调用此实例的两次release方法。使其retainCount降为0，完成回收内存的操作，其 实这也是完全按照内存管理规则办事的好处.

AutoreleasePool是被嵌套的！池是被嵌套的，嵌套的结果是个栈，同一线程只有当前栈顶pool实例是可用的：

|  pool_3  |

|  ---------      |

|  pool_2      |

|  ---------   |


|  pool_1  |

|_______|






	NSAutoreleasePool *pool1 = [[NSAutoreleasePool alloc] init];
		NSAutoreleasePool *pool2 = [[NSAutoreleasePool alloc] init];
		NSAutoreleasePool *pool3 = [[NSAutoreleasePool alloc] init];
	
	NSObject *o = [[NSObject alloc] init] autorelease];
		[pool3 release];
		[pool2 release];
		[pool1 release];
	

我们可以看到其栈顶是pool3，o的autorelease是把当前的release放在栈顶的pool实例管理。。。也就是pool3。
在生命周期短，产生大量放在autoreleasePool中管理实例的情况下经常用此方法减少内存使用，达到内存及时回收的目的。
autorelease pool不是天生的，需要手动创立。只不过在新建一个iphone项目时，xcode会自动帮你写好。autorelease pool的真名是NSAutoreleasePool。
	NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];    NSAutoreleasePool内部包含一个数组（NSMutableArray），用来保存声明为autorelease的所有对象。如果一个对象声明为autorelease，系统所做的工作就是把这个对象加入到这个数组中去。


	ClassA *obj1 = [[[ClassA alloc] init] autorelease]; //retain count = 1，把此对象加入autorelease pool中




NSAutoreleasePool自身在销毁的时候，会遍历一遍这个数组，release数组中的每个成员。如果此时数组中成员的retain count为1，那么release之后，retain count为0，对象正式被销毁。如果此时数组中成员的retain count大于1，那么release之后，retain count大于0，此对象依然没有被销毁，内存泄露。

所有标记为autorelease的对象都只有在这个pool销毁时才被销毁。



