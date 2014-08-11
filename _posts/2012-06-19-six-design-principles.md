---
title: 六大设计原则
layout: post
categories: ['Design-Pattern']
tags: ['Design-Principles']
description: '六大设计原则'
---

**单一职责原则 Single Responsibility Principle**

> There should never be more than one reason for a class to change.

单一职责原则，是指应该有且仅有一个原因引起类的变化。

**里氏替换原则 Liskov Substitution Principle**

> Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.

里氏替换原则，是指只要父类能够出现的地方子类都能够出现，而且替换为子类也不会产生任何异常或错误，使用者根本就不需要知道是父类还是子类。但是，反过来就不戏行了。子类出现的地方，父类就不一定能够适应。

**依赖倒置原则 Dependence Inversion Principle**

> High level modules should not depend upon low level modules. Both should depend upon abstractions. Abstractions should not depends upon details. Details should depend upon abstractions.

依赖倒置原则，是指高层模块不应该依赖底层模块，两者都应该依赖其抽象；抽象不应该依赖细节，细节应该依赖抽象。

**接口分离原则 Interface Segregation Principle**

> Client should not be forced to depend upon interfaces that they don’t use; The dependency of one class to another one should depend on the smallest possible interface.

接口分离原则，是指建立单一的接口，不要建立臃肿庞大的接口。即接口尽量细化，同时接口中的方法尽量少。

**迪米特原则 Law of Demeter / Least Knowledge Principle**

> Only talk to your immediate friends。

迪米特原则，也称最少知识原则，是指一个类应该对自己需要耦合或者调用的类知道的越少越好。

**开闭原则 Open Closed Principle**

> Software entities like classes, modules and functions should be open for extension but close for modifications.

开闭原则，是指一个软件实体如类，模块和函数应该对扩展开放，对修改关闭。
