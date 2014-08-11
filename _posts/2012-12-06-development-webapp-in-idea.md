---
title: 使用Idea社区版开发Web项目
layout: post
categories: ['Work']
tags: ['Idea', 'Maven', 'Jetty']
description: '使用Idea社区版开发Web项目。'
---

在很久很久以前，就听说[IDEA][11]是个绝佳的Java开发工具，奈何囊中羞涩，个人对付费软件只能望而却步；一直善良老实的我，也不好意思去CRACK。所以一直都是使用开源免费的[Eclipse][12]作为工作和学习的IDE。
其实以前也尝试使用过社区版，心里总觉得嘛，功能不全，试试而已，然后就搁下了，所以它一直只是我桌面上的一个的图标而已。。。

但是[IDEA][11]绝不是鸡肋！它已经有很多优秀的功能（只会用小部分功能，待挖掘。。。目前感觉很快，够敏捷，:-)），完全值得我们去尝试，相信很多[Eclipse][12]使用者，特别是Eclipse EE版的使用者，可能会嫌弃它没有Web开发功能，但事实上我们也可以用它来开发Web项目的。

下面会来证明这一点，我会用[IDEA][11] + [Maven][13] + [Jetty][15]来开发Web项目，主要演示下如何调试代码。  
（真希望你对[Maven][13]不陌生，否则花一点时间去学习一下吧，你会喜欢它的。）

1. 首先我们来创建一个[Maven][13]项目，项目类型选择“Maven Module”，输入项目名称“demo”。  
![创建项目-项目类型][1]

2. 选择项目使用的Archetype为“maven-archetype-webapp”，这里也可以随便修改下GroupId等信息。  
![创建项目-Archetype][2]

3. 这一步直接点击“Finish”。  
![创建项目-属性][3]

4. 打开[Maven][13]的配置文件pom.xml，在build节点中添加如下代码，即增加Maven的[Jetty插件][14]。
> &lt;plugins&gt;  
> &nbsp;&nbsp;&nbsp;&nbsp; &lt;plugin&gt;  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;groupId&gt;org.mortbay.jetty&lt;/groupId&gt;  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;artifactId&gt;maven-jetty-plugin&lt;/artifactId&gt;  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;version&gt;6.1.26&lt;/version&gt;  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;configuration&gt;  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;connectors&gt;  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;connector implementation="org.mortbay.jetty.nio.SelectChannelConnector"&gt;  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;port&gt;8080&lt;/port&gt;  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/connector&gt;  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/connectors&gt;  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;scanIntervalSeconds&gt;10&lt;/scanIntervalSeconds&gt;  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/configuration&gt;  
> &nbsp;&nbsp;&nbsp;&nbsp; &lt;/plugin&gt;  
> &lt;/plugins&gt;  

5. 选择工具栏的"Run"-->"Edit Configurations..."，打开“Run/Debug Configurations”窗口，点击绿色的“+”号按钮，在弹出的下拉列表里选择“Maven”。
![配置运行/调试-增加][4]

6. 取一个名称，比如“demo-jetty”；在"Working directory"一栏选择你的工作目录，并在"Command Line"里输入“jetty:run”。然后点击“OK”。  
![配置运行/调试-Maven][5]

7. 到此，配置已经OK了，在工具栏上出现了一个名为“demo-jetty”的运行项，点击后面的调试按钮就可以进行调试了。  
![配置运行/调试-Maven][6]

当然，Web开发还有很多方面啦，这篇仅仅是演示了如何使用[IDEA][11]结合[Maven][13]来开发（着重调试）Web项目。路漫漫其修远兮，吾将上下而求索，我也是初步来尝试[IDEA][11]，希望以后可以把它用好！！

  [1]: {{site.url}}/uploads/2012-12-06/222828_JrZA_80532.png
  [2]: {{site.url}}/uploads/2012-12-06/222904_DxyX_80532.png
  [3]: {{site.url}}/uploads/2012-12-06/223024_yV3j_80532.png
  [4]: {{site.url}}/uploads/2012-12-06/223812_yM8Q_80532.png
  [5]: {{site.url}}/uploads/2012-12-06/223909_KTqX_80532.png
  [6]: {{site.url}}/uploads/2012-12-06/223947_wYLs_80532.png

  [11]: http://www.jetbrains.com/idea/
  [12]: http://www.eclipse.org/
  [13]: http://maven.apache.org/
  [14]: http://docs.codehaus.org/display/JETTY/Maven+Jetty+Plugin
  [15]: http://jetty.codehaus.org/jetty/
