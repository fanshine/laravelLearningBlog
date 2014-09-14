---
title: 开始使用Laravel4
layout: post
categories: ['Laravel4']
tags: ['Laravel 4', 'Install']
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

其次，你也需要确保PHP的最低版本是  ``` 5.3.7 ```，并且安装好``` MCrypt PHP ```扩展，我使用 ```PHP 5.4+ ```和 ``` OS X ```，所以接下来的教程，我假定你已经处理好了开发环境相关的事情。

最后，你需要安装好```Git```，相关资料请自行在网上搜索。

## 安装Laravel 4
那么，我们需要做的第一件事就是从GitHub上下载Laravel的代码。

	git clone -o laravel -b develop https://github.com/laravel/laravel.git cribbb
执行该命令后，会下载Laravel的最新develop版本的代码库到你本地机器的cribbb目录。
```-o laravel```表示远程分支会被命名为laravel，而非默认的origin。这样外面可以随时更新laravel库，同时维护我们自己的origin分支。```-b develop```表示下载develop分支。如果要了解更多关于```git clone```命令的信息，请查看[git文档](http://git-scm.com/book/zh/Git-%E5%9F%BA%E7%A1%80-%E5%8F%96%E5%BE%97%E9%A1%B9%E7%9B%AE%E7%9A%84-Git-%E4%BB%93%E5%BA%93)

一旦Laravel代码库被下载下来以后，进入项目目录

	cd cribbb
	
然后我们需要创建自己的主分支，这样项目开始时间就不会是Laravel代码库的时间了，执行以下命令：

	git checkout --orphan master
	
这样就创建了一个没有父节点的主分支。

同样的，如果想了解更多关于git的命令，请自行阅读[git文档](http://git-scm.com/book/zh/Git-%E5%9F%BA%E7%A1%80-%E5%8F%96%E5%BE%97%E9%A1%B9%E7%9B%AE%E7%9A%84-Git-%E4%BB%93%E5%BA%93)

接下来，我们需要提交这些变化，执行以下命令，以便查看有哪些文件还没有提交：

	git status
	
然后，提交所有文件，加上注释：

	git add -A .
	git commit -m 'Initial commit'
	
现在，如果你想更新laravel，只需要执行下述命令：

	git fetch laravel
	
```git fetch```命令会更新最新的laravel代码库代码。
然后你可以执行下述命令，将最新的laravel代码合并进你的项目：

	git merge --squash -m 'Upgrade Laravel' laravel/develop
	
然后，你还需要安装所有的依赖包：

	composer install
	
之后，你可以通过```composer update```update命令来更新所有已经引用的插件(注意，这里的composer命令，是指的usr/local/bin目录下的composer.phar包)：
	
	composer update
	
最后，执行类似以下命令以设置你自己的```origin```分支：

	git remote add origin git@github.com:你在github上的项目名称.git
	
	
## 配置Laravel
接下来，我们唯一需要做的一点Laravel的配置就是，设置加密串：

	php artisan key:generate
	

## 运行Laravel

至此，Laravel已经成功安装了。如果你是```PHP 5.4```以上版本，你可以在终端里执行如下命令来快速启动一个WebServer，而无需创建虚拟主机：

	php artisan serve
	
现在访问[http://localhost:8080](http://localhost:8080)，你能看的```Hello World!```
如果你不是```PHP 5.4```以上版本，那么你需要配置虚拟主机并将其指向laravel项目的```/public```目录。

恭喜你，你已经成功安装并运行了Laravel 4！