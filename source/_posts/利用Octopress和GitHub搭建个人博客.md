#利用Octopress和GitHub搭建个人博客
网上已经有很多关于搭建Octopress的文章了（可以百度），写这篇文章目的是记录下搭建过程中我遇到的坑

坑一：在Github Page部署是， 执行```rake deploy```总是报错```Updates were rejected because the tip of your current branch is behind```，个人原因是创建blog仓库时，手贱将```Initialize this repository with a README```这个选项个勾选了。
![这是一个Logo图像](/Users/weihaifeng/Desktop/Snip20170426_2.png)
