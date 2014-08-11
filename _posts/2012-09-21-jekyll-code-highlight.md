---
title: Jekyll代码高亮
layout: post
categories: ['Teach']
tags: ['Jekyll', 'Highlight']
description: 'Jekyll代码高亮。'
---

作为一个技术类博客，在博客里粘贴代码是必不可少的事情，代码若没有高亮，可读性真没法说，所以我们需要给自己的博客增加代码高亮的功能。幸运的是，Jekyll提供里代码高亮的功能，我们只需要完成一小部分工作即可。

### 搭建环境 ###

1. Python
2. easy_install
3. Pygments

Jekyll的代码高亮是使用[Pygments][2]来完成的，它是一款语法高亮的[Python][1]包，所以我们首先需要下载并安装[Python][1]。
在MacOS上，完成这件事变得非常简单，因为[Python][1]是MacOS默认安装的:)，可用如下命令检测是否有Python环境：

> python --version  
> \# Python 2.7.3  

安装[Pygments][2]时需要借助[EasyInstall][3]这个工具，这个工具和[Pthon][1]的关系，就像gems和ruby，或者apt-get和ubuntu的关系一样，它可以让你很方便的自动下载、编译、安装和管理[Python][1]包。在[Python][1]的较高版本中，该工具已经自动附带，比如我的版本是2.7.3，easy_install命令已经可以直接使用了，不同平台和环境，可能有所差异(比如Ubuntu上，需要先安装python-setuptools)。若你发现不能使用easy_install命令，记得先安装它。安装好[EasyInstall][3]之后，执行如下命令安装[Pygments][2]：

> easy_install Pygments  

到此，需要的环境已经没有问题了，接下来如何在博客中使用代码高亮？  

### 代码高亮 ###

首先，我们需要生成一个高亮代码的CSS文件，并引入到我们的博客中，生成方式如下：

> pygmentize -S fruity -f html > syntax.css

然后，在博客中使用代码高亮，高亮代码的模板是这样的：

> \{_%_ highlight *词法分析器* %\}  
> 需要高亮的代码  
> \{_%_ endhighlight %\}  

词法分析器是指你需要高亮的代码是何种语言，比如说**Shell脚本**的词法分析器是**sh**，**Java**的词法分析器是**java**。支持的词法分析器可以在官方文档[Available lexers][4]找到。

例如你要高亮Java版的HelloWorld，只需要把如下代码粘贴到你的博客中：

> \{_%_ highlight java %\}  
> public class Hello {  
> &nbsp;&nbsp;public static void main(String[] args) {  
> &nbsp;&nbsp;&nbsp;&nbsp;System.out.println("Hello World!");  
> &nbsp;&nbsp;}  
> }  
> \{_%_ endhighlight %\}  

在我的博客中，显示效果如下：

{% highlight java %}
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello World!");  
    }
}
{% endhighlight %}

它看起来还不错，代码的可读性大大提高了。

### Github Pages ###

[GitHub Pages][5]也是支持**\{_%_ highlight %\}**标记的，提交上去的博客，生成的代码html代码和你本地生成的相同，另外又使用里相同的样式，所以不会有任何问题。


[1]: http://www.python.org/ "Python"
[2]: http://pygments.org/ "Pygments"
[3]: http://peak.telecommunity.com/DevCenter/EasyInstall "EasyInstall"
[4]: http://pygments.org/docs/lexers/ "Available lexers"
[5]: http://pages.github.com/ "GitHub Pages"

