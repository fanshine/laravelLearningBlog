---
title: MySQL 事件
layout: post
categories: ['Database']
tags: ['MySQL', 'Event']
description: 'MySQL 事件'
---

MySQL 5.1 增加了"Event(事件)"的特性，这个特性看来很不错。下面是一个简单的示例：

{% highlight sql %}

set global event_scheduler = 1;
drop event if exists event_test;
create event
	event_test
on schedule
	every 1 second
do
	update `user` set create_at = now() where id = 1;

{% endhighlight %}

这样，每秒钟就会执行指定的SQL语句，很不错的功能。  
简单来说，Event就是数据库里的计划任务，可以用来做数据汇总等周期性的任务了。

想更多关于Event的知识，请猛击[这里](http://dev.mysql.com/doc/refman/5.1/en/create-event.html).