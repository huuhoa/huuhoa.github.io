---
layout: post
title: "Delay function call with ReactiveCocoa"
date: 2014-03-29 11:14:02 +0700
comments: true
categories: [ReactiveCocoa]
---
Delay a function call is possible with ReactiveCocoa with -[RACSignal delay:] 

``` objective-c
- (void)delayLogString:(NSString *)string timeInterval:(NSTimeInterval)timeInterval {
	[[[RACSignal empty] delay:timeInterval] subscribeComplete:^{
		NSLog(@"This log message is printed out after %f seconds", timeInterval);
 	}];
}
```
