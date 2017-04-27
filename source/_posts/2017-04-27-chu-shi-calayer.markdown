---
layout: post
title: "初识CALayer"
date: 2017-04-27 10:14:04 +0800
comments: true
categories: iOS
---

###一、Layer简介
     CALayer是定义在QuartzCore框架中的(Core Animation)，它是绘图和动画的基础，是在3D空间中的2D平面。CALayer管理的几何（例如rotate，transfrom），内容（image等），和可视属性（backgroundColor，alpha）等信息。<!--more-->CALayer主要通过管理bitmap来维护自己的状态信息，从这一点上来说，Layer可以看作对象模型，因为他们主要用来管理数据。
###二、Layer与bitmap的关系
      Layer是基于bitmap的，它会捕获View要呈现的内容，然后cache在一个bitmap中，这个bitmap可以看作一个对象。这样每次进行操作，例如平移旋转等，只是bitmap的矩阵运算。

      由于基于Layer的绘制是处理静态的Bitmap的，而bitmap的处理又是GPU所擅长的，所以它的效率要比基于View绘制的高很多，因为基于View绘制的每次都要进行drawRect的调用重新绘制。

###三、UIView与CALayer的关系
      既然说CALayer ，那么UIView肯定要提一下， UIView是iOS系统中界面元素的基础，所有的界面元素都继承自它。在创建UIView对象时，UIView内部会自动创建一个图层(即CALayer对象)，通过UIView的layer属性可以访问这个层。UIView本身更像是一个CALayer的管理器，访问它的跟绘图和跟坐标有关的属性，例如frame，bounds等等，实际上内部都是在访问它所包含的CALayer的相关属性。

      另外UIView和CALayer最大的区别就是UIView可以接受用户输入（例如触摸）而CALayer不可以，CALayer单独并不能呈现出任何可视的内容，必须依托于UIView。CALayer只是几何上呈现给用户的东西，它较为轻量，通常采用Cache技术，对资源消耗也较小。

      UIView和CALayer关系图如下：
      
![关系图](http://cc.cocimg.com/api/uploads/20161204/1480865231251244.png)
###四、anchorPoint和position
   和UIView不同，Layer主要由三个属性来设置位置（极少用```Frame： ```）

- bounds                 设置大小
- anchorPoint         设置锚点（锚点对后续的layer动画有很大影响）
- position                锚点在superLayer中的位置

      这样说有点抽象，我们看看以下的图就了解了对于iOS来说，坐标系如图，archPoint（x,y）的两个值通常取0.0-1.0,默认值是（0.5，0.5）这里的值可以看作所占用x的比例，比如默认的0.5，0.5就是在x的中间和y的中间。
￼![20150110130108359.png](http://upload-images.jianshu.io/upload_images/2782212-f61aade513ffd51e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

      而position则是AnchorPoint在super layer中的位置
如下图
![20150110130534295.png](http://upload-images.jianshu.io/upload_images/2782212-071d76aaa3517d68.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###五、管理Layer内容的几个函数
- addSublayer:
- insertSublayer:above:
- insertSublayer:atIndex:
- insertSublayer:below:
- removeFromSuperlayer
- replaceSublayer:with:

###六、Layer支持继承，支持添加Sublayer，支持对sublayer进行层次调整

- CAEmitterLayer            发射器层，用来控制粒子效果
- CAGradientLayer           梯度层，颜色渐变
- CAEAGLayer                用OpenGL ES绘制的层
- CAReplicationLayer      用来自动复制sublayer
- CAScrollLayer              用来管理可滑动的区域
- CAShapeLayer             绘制立体的贝塞尔曲线
- CATextLayer                 可以绘制AttributeString
- CATiledLayer                用来管理一副可以被分割的大图
- CATransformLayer        用来渲染3D layer的层次结构



文章参考：[《 IOS SDK详解之CALayer（一）》](http://blog.csdn.net/hello_hwc?viewmode=contents)、[《初探CALayer属性》](http://www.jianshu.com/p/b64f9a1bdd1b) 