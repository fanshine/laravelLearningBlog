---
title: Lucene简介和入门
layout: post
categories: ['Hello']
tags: ['HelloWorld', 'Lucene']
description: 'Lucene简介和入门'
---

这几天我花了些时间去研究了下Lucene，读了很多博客和文章，也写了些示例代码，对全文检索以及使用到的技术都有了认识，感觉非常好。  
Lucene是当今非常流行的全文检索工具，对于我们开发者来说，给应用添加一个搜索功能确实容易很多了，希望在接下来的项目里可以一施拳脚。  
接下来对Lucene进行一个初步的介绍，并附带一个简单的示例程序。

### Lucene 简介 ###

Lucene是一个基于Java的高性能、可伸缩的全文信息检索库，它提供了简单而强大的API，让你很容易为文档创建索引，并基于创建的索引进行搜索。  
Lucene是由资深全文索引/检索专家Doug Cutting创建的，开始是给自己的博客程序使用，后来开源出来，如今它已成为Apache软件基金会的顶级项目，也成为最受欢迎的Java全文信息检索工具。

### Lucene 原理 ###
Lucene主要完成两件事：

1. 创建索引
2. 基于索引搜索。  

创建搜索是一件非常关键的一步，Lucene 采用的是一种称为反向索引（inverted index）的机制。
先说下什么是正向索引（若是有这个概念的话），给你一些文档，让你找到里面的词/短语，类似小学课堂上，老说问：“同学们，有谁来总结下这篇文章讲了什么？”，这是一个从文档到词/短语的过程。  
而反向索引刚好相反，它是指从词/短语到文档的过程，举一个例子：给出“Java”这个关键字，找到所有Java相关的文档。

当索引创建已经创建好之后，搜索文档就是先到索引库里去找索引，然后根据找到的索引找到文档。整个过程可以用下图表示：
![Lucene典型应用结构图]({{site.url}}/uploads/2012-10-19/lucene.png)

### 入门示例 ###

**创建索引**
{% highlight java %}
public void index() throws IOException {
	try {
		String docsDir = "src";
		String indexDir = "target/index";
		Directory directory = FSDirectory.open(new File(indexDir));
		Analyzer analyzer = new StandardAnalyzer(Version.LUCENE_40);
		IndexWriterConfig config = new IndexWriterConfig(Version.LUCENE_40, analyzer);
		IndexWriter writer = new IndexWriter(directory, config);
		indexDocs(writer, new File(docsDir));
		writer.close();
	} catch (IOException e) {
		e.printStackTrace();
	}
}

private void indexDocs(IndexWriter writer, File path) throws IOException {
	if (path.isDirectory()) {
		File[] files = path.listFiles();
		if (files != null) {
			for (int i = 0; i < files.length; i++) {
				indexDocs(writer, files[i]);
			}
		}
	} else {
		Document doc = new Document();
		doc.add(new StringField("name", path.getName(), Field.Store.YES));
		doc.add(new StringField("path", path.getPath(), Field.Store.YES));
		doc.add(new TextField("contents", new FileReader(path)));
		System.out.println("adding " + path);
		writer.addDocument(doc);
	}
}
{% endhighlight %}
**基于索引搜索**  
{% highlight java %}
public void search() {
	String index = "target/index";
	String searchField = "contents";
	String keyWorld = "String";
	try {
		IndexReader reader = DirectoryReader.open(FSDirectory.open(new File(index)));
		IndexSearcher searcher = new IndexSearcher(reader);
		Analyzer analyzer = new StandardAnalyzer(Version.LUCENE_40);
		QueryParser parser = new QueryParser(Version.LUCENE_40, searchField, analyzer);
		Query query = parser.parse(keyWorld);
		System.out.println("Search [" + keyWorld + "]:");
		TopDocs results = searcher.search(query, 10);
		ScoreDoc[] hits = results.scoreDocs;
		for (int i = 0; i < hits.length; i++) {
			Document doc = searcher.doc(hits[i].doc);
			System.out.println(doc.get("name"));
		}
		reader.close();
	} catch (Exception e) {
		e.printStackTrace();
	}
}
{% endhighlight %}

项目基于Maven，完整源码请点击下载：[lucene.zip][2]


[1]: http://lucene.apache.org "Lucene"
[2]: {{site.url}}/uploads/2012-10-19/lucene.zip "lucene.zip"

