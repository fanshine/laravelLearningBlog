---
title: 教你一步一步搭建Jekyll博客【Mac】
layout: post
categories: ['Teach']
tags: ['Jekyll']
description: '教你一步一步搭建Jekyll博客【Mac】。'
---

现在我使用的博客是用[Jekyll](https://github.com/mojombo/jekyll)搭建的，放在[Github](https://github.com)上，我也用它来记录我的工作、学习的心得，以及生活的点滴，目前它用起来还不错，我很喜欢。
现在回想起来，当初搭建它的过程蛮**“曲折”**的，网上有不少的资料，但是没有完整的、一步一步式的文章，我一直看官方的文档，也研究了不少其他博客的代码，也花了很多时间来修改它，总算有些心得，现在把它记下来，让需要的人可以节省宝贵的时间。
当然了，你也可以选择[JekyllBootstrap](http://jekyllbootstrap.com)来搭建博客，它应该可以很快让你开始写博客了，帮你绕过诸多的麻烦，不过我总是喜欢自己来动手完成这个事情，所以这篇文章也是写给和我有相同想法的人。

我使用的是Mac搭建的，Mac自带了Ruby-1.8.7，Python-2.7.2，所以省了这些软件的安装，若是其他平台的话，需要先安装相关的环境。

---

1. **升级gem**
	> sudo gem update --system
2. **修改gem源**
	某些gem源很难安装成功，大多数是网络问题，我尝试了下面两个源，最终顺利通过了，建议选择适当的源安装。
	> gem sources  \#查看源列表
	> gem sources --remove http://xxx.org \#移除不需要的他源
	> gem sources --add http://gems.rubyforge.org \#添加rubyforge源
	> gem sources --add http://gems.github.com \#添加github源
3. **安装Jekyll**
	安装Jekyll可能会遇到若干错误，这一步我也遇到了诸多麻烦，多数是网络不给力，老是超时，后来我在深夜网络速度好的时候尝试，终于安装成功了。若这一步遇到其他错误，建议把错误信息直接放到Google里搜索，若是把你带你到了[stackoverflow](http://stackoverflow.com)上，一般都能教容易解决问题。
	> sudo gem install jekyll
4. **创建默认的目录结构**
	安装好jekyll之后，我们可以来写博客了，首选需要创建基本的目录结构，省去繁琐的命令，创建之后的目录结构如下：
	> .
	> |-- \_includes
	> |-- \_layouts
	> |-- |-- default.html
	> |-- |-- post.html
	> |-- \_posts
	> |-- |-- 2012-08-15-hello-world.md
	> |-- \_site
	> |-- \_config.yml
	> |-- index.html
5. **测试**
	尝试启动本地服务器，看环境安装，以及目录的创建是否都OK。
	> jekyll --server
	若本地服务器启动正常，打开浏览器，输入地址：[http://localhost:4000](http://localhost:4000)，若没有问题的话，可以看到index.html的内容。
	另外，启动服务的服务的时候，建议修改Jekyll配置文件_configy.yml，增加如下代码：
	> auto: true
	该代码让Jekyll自动检测修改，否则每次修改后，你都需要重新启动服务器才能看到变化，比较麻烦。更多Jekyll的配置，请看[官方配置说明](https://github.com/mojombo/jekyll/wiki/configuration)。
7. **定义默认的布局文件**
	一起看起来都还OK？那么我们来开始完善我们的博客吧，首先我们需要一个模板，这个模板供所有页面使用，它会引入需要的css，javascript等文件，以及导航条，版权等信息。我想你应该熟悉这个模板的样子，所以我只想说明其中你可能需要注意的两点，具体细节可以参考下我的[default.html](https://github.com/{{site.author.name}}/{{site.author.name}}.github.com/blob/master/_layouts/default.html)。
	* **标题** 你可能需要自定义你的标题，我是这样定义我的博客标题的：
		> \{_%_ if page.title %\} \{\{ page.title \}\} - \{_%_ endif %\} Laravel知识整理
		如果页面定义了标题的话，它会使用该标题，并跟上“ - Laravel知识整理”，作为浏览器的标题，否则就直接将“Laravel知识整理”作为浏览器的标题。
	* **内容占位符** 使用\{\{content\}\}来定义内容占位符，使用该模板时，内容将替换该模板里的占位符。
	编写模板的时候，需要用到[Liquid](https://github.com/Shopify/liquid)模板引擎，它学习起来并不难，下面两篇文章浏览一遍，应该就可以快速上手了：
	* [Liquid for Designers](https://github.com/shopify/liquid/wiki/liquid-for-designers)
	* [Liquid Extensions](https://github.com/mojombo/jekyll/wiki/Liquid-Extensions)
8. **定义显示文章的布局文件**
	我们还需要为每篇文章制定一个模板，制定方式和制定默认模板default.html是一样的，甚至我们可以套用默认的模板来简化工作，只需要在post.html前面增加如下代码：
	> \---
	> layout: default
	> \---
	这样，post的布局就使用了默认的模板，只需要针对博文制定下模板就可以了，比如说标题，内容，日期如何显示等，具体细节可以参考下我的[post.html](https://github.com/{{site.author.name}}/{{site.author.name}}.github.com/blob/master/_layouts/post.html)。需要注意的是：post里也有可以使用\{\{conten\}\}，但是这里该变量已经不是占位符了，可以说它是一个变量，即post\.content，代表了博文的正文内容。
	完成这一步后，可以打开[hello-world](http://localhost:4000/2012-08-15/hello-world.html)页面看看你的模板是否都起作用了。
9. **定义首页**
	我们的首页依然是空洞的index.html的内容，这个可不是我们希望的，那么，我们一起来修改修改。
	首页应该显示什么呢？可以显示博客列表，带分页功能，或者只显示最近的N篇博客。
	我们就来实现第二种吧，简单实用，和我目前的做法相同。至于如何实现分页，感兴趣的朋友可以去阅读相关知识，自己尝试实现 :-)
	我们只需要修改index.html页面，增加如下代码：
	> \{_%_ for post in site.posts limit:5 %\}
	> \<h2\>\<a class="post_title" href="\{\{post.url\}\}">\{\{post.title\}\}\</a\>\</h2\>
	> \<div class="post-content"\>\{\{post.content\}\}\</div\>
	> \{_%_ endfor %\}
	该代码会显示最近的5篇博文。
	另外，记得引入默认的布局模板，并设置好页面的标题，这样，整个博客的风格看起来就一致了，我们也指定了页面的标题为“首页”，那么首页显示的时候，就会将“首页 - Laravel知识整理”作为浏览器的标题了。
	> \---
	> layout: default
	> title: 首页
	> \---
	具体细节可以参考下我的[index.html](https://github.com/{{site.author.name}}/{{site.author.name}}.github.com/blob/master/index.html)。
10. **按日期归档博客**
	每个博客都应该有一个归档的功能。我们也来做一个吧。新建archives.html，增加如下代码：
	> \{_%_ capture archives_year %\}
    > &nbsp;&nbsp;&nbsp;&nbsp;\{\{ 'now' | date: '%Y' \}\}
    > \{_%_ endcapture %\}
    >
    > \{_%_ for post in site.posts %\}
    > &nbsp;&nbsp;&nbsp;&nbsp;\{_%_ capture post_year %\}
    > &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\{\{ post.date | date: '%Y' \}\}
    > &nbsp;&nbsp;&nbsp;&nbsp;\{_%_ endcapture %\}
    > &nbsp;&nbsp;&nbsp;&nbsp;\{_%_ if archives_year != post_year %\}
    > &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\{_%_ assign archives_year = post_year %\}
    > &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\<h2\>\{\{ archives_year \}\}\</h2\>
    > &nbsp;&nbsp;&nbsp;&nbsp;\{_%_ endif %\}
    > &nbsp;&nbsp;&nbsp;&nbsp;\{\{ post.date | date: "%m-%d" \}\} - \<a href="\{\{post.url\}\}">\{\{ post.title \}\}\</a\> \</br\>
    > \{_%_ endfor %\}

    该代码会将所有的博客按照日期（年份）进行归档。上面的代码看起来会是这个样子：
    ![归档](/uploads/2012-08-15/archives.png)
    同时，我们也为归档页面制定布局模板和标题：
	> \---
	> layout: default
	> title: 归档
	> \---
	具体细节可以参考下我的[archives.html](https://github.com/{{site.author.name}}/{{site.author.name}}.github.com/blob/master/archives.html)。
11. **代码高亮**
	见我另外一篇博客：[Jekyll代码高亮](/2012-09-21/jekyll-code-highlight.html)
12. **集成第三方评论**
	（待完成）
13. **后续工作**
	现在差不多可以让你开始写博客了，强烈建议你把它发布到[GitHub Pages](http://pages.github.com)上去。这里有一个使用Jekyll搭建的博客[列表](https://github.com/mojombo/jekyll/wiki/Sites)，你会发现，很多都是放在[GitHub Pages](http://pages.github.com)上的。
	另外，目前的博客还不算一个完善的博客，你应该继续添加如下的文件：
	* 404.html
	* about.html
	* rss.xml（atom.xml）
	* favicon.ico
	* robots.txt
	* sitemap.xml
	* search.xml

	它们需要你继续花时间去完成，我就不详细写出来了，对于一个简单的博客，上面介绍的已经足够了。

---

整个过程我写得比较简单实用，也记录了主要的步骤和思路，若你已经可以搭建一个基于Jkeyll的博客，这篇博客的目的基本达到了。但若有不正确的地方，欢迎指正。

参考阅读：

1. [Blogging Like a Hacker](http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html)
2. [Jekyll Wiki](https://github.com/mojombo/jekyll/wiki/_pages)
3. [Liquid Wiki](https://github.com/Shopify/liquid/wiki)
4. [GitHub Help](https://help.github.com/categories/20/articles)
