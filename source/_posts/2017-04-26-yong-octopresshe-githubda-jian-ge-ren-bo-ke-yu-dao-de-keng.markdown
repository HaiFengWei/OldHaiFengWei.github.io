---
layout: post
title: "用Octopress和GitHub搭建个人博客遇到的坑"
date: 2017-04-26 09:36:38 +0800
comments: true
categories: octopress
---
网上已经有很多关于搭建Octopress的文章，所以我写篇文章目的记录下我搭建blog过程中遇到的坑，如有人遇到相同问题可以参考一下😁。<!--more-->


####坑一、GithubPage部署时执行```rake deploy```时报错：

错误信息有这么一句```Updates were rejected because the tip of your current branch is behind```
这个错误是我在创建仓库时手贱将```Initialize this repository with a README```这个选项给选中了，这样会导致本地当前版本低于服务端的版本，执行```rake deploy```发布博文到GitHub Pages失败

 ![图片](https://haifengwei.github.io/images/Snip20170426_2.png)
 

###坑二、在头部导航栏添加Categories:
 
1、设置导航栏

导航栏的设置在```source\_includes\custom\navigation.html```
我们可以将Blog和Archives修改为首页和归档，也可以在此添加一个标签页，此时应使用命令```rake new_page['about']```创建一个页面，页面路径为```source\about\index.markdown```;
修改后的文件如下：

```
<ul class="main-navigation"> 
  <li><a href="{{ root_url }}/">首页</a></li> 
  <li><a href="{{ root_url }}/blog/archives">归档</a></li> 
  <li><a href="{{ root_url }}/about">关于</a></li> 
</ul>
```

2、生成Categories

可以参考下[《Octopress博客设置》](http://fwhyy.com/2013/05/octopress-blog-setting/) 、[《为octopress添加分类(category)列表》](http://codemacro.com/2012/07/18/add-category-list-to-octopress/)和问度娘（✿◡‿◡）
 
3、在头部导航栏添加Categories

百度了一下，全都是说怎么在侧边导航栏怎么添加Categories（老铁，扎心了）。

于是我到处找博文看，就这么找了半天终于看到这么一篇文章[《为octopress添加tag cloud》](http://codemacro.com/2012/07/18/add-tag-to-octopress/)和，其中有这么一段代码
 
 		
 ```
 <section>
  <h1>Tags</h1>
  <ul class="tag-cloud">
    {\% tag_cloud font-size: 90-210%, limit: 10, style: para \%}
  </ul>
</section>
 ```
 感觉有点像，于是我就在```source\Categories\index.markdown```里写了一这么段东西

```
---
layout: page
title: Categories
navbar: Categories
footer: false
---
{\% category_list font-size: 90-210%, limit: 1000, style: para \%}
```


没想到还就成了。