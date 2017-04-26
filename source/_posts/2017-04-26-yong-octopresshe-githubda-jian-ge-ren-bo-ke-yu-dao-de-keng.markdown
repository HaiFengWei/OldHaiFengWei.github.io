---
layout: post
title: "用Octopress和GitHub搭建个人博客遇到的坑"
date: 2017-04-26 09:36:38 +0800
comments: true
categories: 
---
网上已经有很多关于搭建Octopress的文章，所以我写篇文章目的记录下我搭建blog过程中遇到的坑。

坑一、GithubPage部署时执行```rake deploy```时报错：

错误信息有这么一句```Updates were rejected because the tip of your current branch is behind```
这个错误是我在创建仓库时手贱将```Initialize this repository with a README```这个选项给选中了，这样会导致本地当前版本低于服务端的版本，执行```rake deploy```发布博文到GitHub Pages失败

 ![示例图](https://haifengwei.github.io/images/Snip20170426_2.png)
 