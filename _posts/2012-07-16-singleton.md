---
title: 设计模式之单例模式
layout: post
categories: ['Design-Pattern']
tags: ['Singleton']
description: 'Singleton'
---

单例模式，顾名思义，就是只有一个实例。  
这个模式确保某一个类只有一个实例，而且自行实例化并向整个系统提供这个实例。

下面是一个简单、常见的单例模式的写法：

{% highlight java %}
public class Singleton {
	private static Singleton singleton = new Singleton();
	private Singleton() {
		new Error("Don't instance me.");
	}
	public static Singleton getInstance() {
		return singleton;
	}
	public void operate() {
		System.out.println("Do your stuff.");
	}
}
{% endhighlight %}

单例模式还有另外一种写法，会用到双检测锁（Double-Ckeck Locking）。  
双检测锁是为了避免单例类在多线程环境中产生出多个实例，破坏单例模式。为什么需要使用双检测锁见这篇文章分析：[http://en.wikipedia.org/wiki/Double-checked_locking#Usage_in_Java](http://en.wikipedia.org/wiki/Double-checked_locking#Usage_in_Java)。

{% highlight java %}
public class Singleton {
	private static Singleton singleton;
	private Singleton() {
		new Error("Don't instance me.");
	}
	public static Singleton getInstance() {
		// Double-Check Locking
		if (singleton == null) {
			synchronized (Singleton.class) {
				if (singleton == null) {
					singleton = new Singleton();
				}
			}
		}
		return singleton;
	}
	public void operate() {
		System.out.println("Do your stuff.");
	}
}
{% endhighlight %}

其实这两种写法没有多大差别，只是在初始单例变量的时间不同。  
第一种是推荐的写法，但在有些情况下，比如说需要延迟初始化单例变量，或者单例变量需要依赖其他变量，可能就需要第二种写法了。
