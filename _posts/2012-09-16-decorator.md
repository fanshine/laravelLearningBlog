---
title: 设计模式之装饰器模式
layout: post
categories: ['Design-Pattern']
tags: ['Decorator']
description: ’Decorator。'
---

装饰模式属于结构性模式，它的意图是在一个对象的外围创建一个称为装饰器的封装，动态地给这个对象添加一些额外的功能。 
装饰模式常用来替代继承，我们知道，继承可以解决很多实际的问题，但是继承缺少灵活性，在多重继承之后，你就知道维护你的代码有多麻烦；继承也容易引起类膨胀，需求变动或者扩展是常有的事情。而装饰模式可以用一种灵活的方式给类增加新的特性，它的重用性和扩展性也很不错。

先来看看通用代码：

{% highlight java %}
public interface Component {
	public void behavior();
}

public class ConcreteComponent implements Component {
	@Override
	public void behavior() {
		System.out.println("Component.");
	}
}
{% endhighlight %}

{% highlight java %}
public abstract class Decorator implements Component {
	private Component component;
	public Decorator(Component component) {
		this.component = component;
	}
	@Override
	public void behavior() {
		this.component.behavior();
	}
}

public class ConcreteDecorator extends Decorator {
	public ConcreteDecorator(Component component) {
		super(component);
	}
	@Override
	public void behavior() {
		super.behavior();
		this.addedBehavior();
	}
	private void addedBehavior() {
		System.out.println("ConcreteDecorator: Added Behavior.");
	}
}
{% endhighlight %}

客户端使用的时候，创建需要装饰的组件（Component），然后把该组件交给具体的装饰器（ConcreteDecorator）进行装饰一番，装饰之后的组件就用了新的特性。若是实现了多个装饰器，还可以进行多次装饰，每次都是把组件交给装饰器进行装饰，这样就能得到具有复杂功能的组件。具体代码如下：

{% highlight java %}
public class Client {
	public static void main(String[] args) {
		Component component = new ConcreteComponent();
		component = new ConcreteDecorator(component);
		component.behavior();
	}
}
{% endhighlight %}

接下来对涉及到的四种角色做一个说明：

1. Component：组件类接口，我们需要去装饰一个组件，这个即是我们需要去装饰的组件的接口。
2. ConcreteComponent：实现Component接口的具体组件类，它完成了基本的功能，但还需要继续扩展，扩展就由装饰器来做咯。
3. Decorator：抽象类装饰器，它一般不会完成任何功能，即用它装饰之后的组件没有有任何变化。
4. ConcreteDecorator：继承Decorator，实现具体的功能，如为需要装饰的组件增加特性，增加属性等。
