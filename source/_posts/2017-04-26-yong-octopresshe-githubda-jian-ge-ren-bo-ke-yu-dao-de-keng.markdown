---
layout: post
title: "用Octopress和GitHub搭建个人博客遇到的坑"
date: 2017-04-26 09:36:38 +0800
comments: true
categories: octopress
---
     网上已经有很多关于搭建Octopress的文章，所以我写篇文章目的记录下我搭建blog过程中遇到的一些问题（注：我认为的坑），如有人遇到相同问题可以参考一下😁。<!--more-->


####一、GithubPage部署时执行```rake deploy```时报错：

     错误信息有这么一句```Updates were rejected because the tip of your current branch is behind```
这个错误是我在创建仓库时手贱将```Initialize this repository with a README```这个选项给选中了，这样会导致本地当前版本低于服务端的版本，执行```rake deploy```发布博文到GitHub Pages失败

 ![图片](https://haifengwei.github.io/images/Snip20170426_2.png)
 

###二、在头部导航栏添加Categories:
 
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

     于是我到处找博文看，就这么找了半天终于看到这么一篇文章[《为octopress添加tag cloud》](http://codemacro.com/2012/07/18/add-tag-to-octopress/)，发现添加云标签的原理是借鉴Categories，而且可以添加在任意位置。也就是说tag cloud可以添加在任意位置，那么Categories也可以。其中[《为octopress添加tag cloud》](http://codemacro.com/2012/07/18/add-tag-to-octopress/)有这么一段代码（去掉\\），是为tag cloud写一个页面出来
 
 		
 ```
 <section>
  <h1>Tags</h1>
  <ul class="tag-cloud">
    {\% tag_cloud font-size: 90-210%, limit: 10, style: para \%}
  </ul>
</section>
 ```
     我就仿照这段代码在```source\Categories\index.markdown```里写成这样（去掉\\）

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

###三、如何文章详情页添加评论栏:
     我这里的评论是用的友言，至于集成友言可参考巧神的[《象写程序一样写博客：搭建基于github的博客》](http://blog.devtang.com/2012/02/10/setup-blog-based-on-github/)，我这里是将```weibo_share```改为```share_comment```。

     至于在哪里添加评论栏位置，只是描述一下我的问题，可能对于你们并不一定适用。

     我集成的第三方主题是[《abacus theme》](https://github.com/bhrigu123/abacus)，文章详情页是/source/_layouts/post.html，里面可以添加和删除文章详情页的控件（我特么一个一个文件试过来发现的o(╯□╰)o）。那么，添加评论栏也理所当然这里了，于是我修改了下面一段代码（去掉\\）

```
 </article>
    {% if site.disqus_short_name and page.comments == true %}
      <section>
        <h2>Comments</h2>
        <div id="disqus_thread" aria-live="polite">{\% include post/disqus_thread.html \%}</div>
      </section>
    {% endif %}
    {\% include post/share_comment.html \%}
```
     这里主要是在详情页尾添加一句``` {\% include post\/share_comment.html \%}```

     另外将/_config.yml里的Comments也设置下，```disqus_short_name```得值随意写，```disqus_show_comment_count```值为true（如下）。

```
# Disqus Comments
disqus_short_name: ******
disqus_show_comment_count: true
```

###四、设置页面和控件的属性位置：
     /sass里是设置页面和控件的属性位置，至于有什么效果，自己试试就清楚了。
     

######     注：本人不懂这方面技术，如有错误的地方，请指正。