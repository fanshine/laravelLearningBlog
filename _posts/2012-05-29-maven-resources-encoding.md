---
title: 为Maven指定资源文件的编码
layout: post
categories: ['Maven']
tags: ['Encoding']
description: '为Maven指定资源文件的编码'
---

使用Maven构建项目的时候，常常会遇到这样的警告：

> [WARNING] Using platform encoding (GBK actually) to copy filtered resources, i.e. build is platform dependent!

如何解决呢？修改pom.xml文件，增加下面的代码，为Maven指定资源文件的编码：

{% highlight xml %}
<!-- pom.xml -->
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
</properties>
{% endhighlight %}

这样，你会发现，构建项目的时候输出信息变成了：

> [INFO] Using 'UTF-8' encoding to copy filtered resources.

嗯~我喜欢没有任何警告的信息输出！  
事实上，Maven还有些默认设置可能也不适合你的项目，也需要去修改默认配置。比如说：

1. JDK版本号
2. 编译器的版本号
