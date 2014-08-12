---
title: 开始使用Laravel4
layout: post
categories: ['Laravel4']
tags: ['MySQL', 'Event']
description: '开始使用Laravel4'
---

[Laravel 4](https://github.com/laravel/framework) 是流行的PHP框架[Laravel](http://laravel.com/)的一个最新升级版本。Laravel是一个“干净优雅”的用于Web开发的现代PHP框架。受[Ruby on Rails](http://rubyonrails.org/)，以及[Symfony](http://symfony.com/)框架的启发，Laravel 4致力于让你使用近年来日益完善的PHP新技术来开发好的web程序。

Laravel 4脱胎于[Laravel 3](http://laravel.com)，但是对上一个版本又做了很多的改进。现在，Laravel 4是一个经过了大量测试，并且在维持干净优雅的语法结构的基础上，继续添加新的组件和特性的框架。

Laravel 4通过[Composer](http://getcomposer.org/)来管理更新和独立的第三方组件。现在可以更自由的混合匹配其他的PHP组件。Laravel 4本身也引用了一些目前最流行的来自Symfony框架的组件，并没有重复的制造轮子。

所有这一切使得Laravel 4成为你下一个项目的所需框架的最好的选择。

Laravel 4目前还没有正式发布，但是你已经可以开始尝试使用它了。(文章写于2013-04-29，现在Laravel 4.2都已经正式发布了)

在这个教程中，我会展示所有Laravel 4的技巧以实现一个项目。

这是我第二次写Laravel 4的教程。第一次我根据[Laravel 4的文档](http://four.laravel.com)写了如何配置起一个Laravel 4的项目。然而，在读了[Chris Fidao](https://twitter.com/fideloper)写的[教程](http://fideloper.com/best-way-to-install-laravel4)后，我决定重新写一个教程，但是和[Aaron Kuzemchak](https://twitter.com/akuzemchak)写得[教程](https://gist.github.com/akuzemchak/5210425)有一点区别。所以，感谢前两位的贡献，我得以在此基础上继续深入探讨如何使用Laravel 4。

## 环境要求

Laravel 4基本无需额外的配置，但是在本机使用还是对环境有一定的要求。

首先，你需要安装[Composer](http://getcomposer.org/)。Composer是一个PHP的包管理工具，允许你很方便的在自己的工程中管理不同的PHP组件。如果你没能把Composer配置起来，可以看一下[这篇文章](http://culttt.com/2013/01/07/what-is-php-composer/)

其次，你也需要确保PHP的最低版本是{% highlight php %} 5.3.7 {% endhighlight %}，并且安装好{% highlight php %}MCrypt PHP{% endhighlight %}扩展