---
title: no branches ready for upload
layout: post
categories: ['Git']
tags: ['Git']
description: 'Git - no branches ready for upload'
---

You must do the following steps:

{% highlight sh %}
$ repo abandon <branch> <project>
$ repo start <branch> <project>
$ git reset --hard <latest-github-commit-id>
  (git add/commit)
$ repo upload <project>
{% endhighlight %}
