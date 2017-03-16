---
layout: post
title:  "纯原生 App开发模式还能走多久？"
date:   2017-03-16 19:10:05
categories: Android
excerpt: Android开发。
---

* content
{:toc}

>###### 文中涉及到的几个概念（信息来自百度百科和百度知道）：
* Native App（原生APP）开发：该开发针对IOS、Android等不同的手机操作系统要采用不同的语言和框架进行开发，该模式通常是由“云服务器数据+APP应用客户端”两部份构成，APP应用所有的UI元素、数据内容、逻辑框架均安装在手机终端上。 
* Web App开发：即是一种框架型APP开发模式（HTML5  APP 框架开发模式），该开发具有跨平台的优势，该模式通常由“HTML5云网站+APP应用客户端”两部份构成，APP应用客户端只需安装应用的框架部份，而应用的数据则是每次打开APP的时候，去云端取数据呈现给手机用户。
* Hybrid App：是指介于web-app、native-app这两者之间的app,它虽然看上去是一个Native App，但只有一个UI WebView，里面访问的是一个Web App。


# 一、Web App体验
最近因为比赛需要，由于时间不怎么充裕，便利用PHP写了服务器端，jQuery Mobile写了一个整个 APP的框架（只是简单的框架）和内容，然后再借助android的WebView控件显示页面，就这样传说中的Web App就新鲜出炉了。当然这只是简单的一个小应用，真正的Web App开发还牵涉到更多的知识，这里我们不做讨论。

![Web App](http://upload-images.jianshu.io/upload_images/3845101-1272f5ee8a3fa334.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![Web App](http://upload-images.jianshu.io/upload_images/3845101-5aa2f40e80ce0be9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

虽然是如此简单的一个小应用，却也五脏俱全。实现了按钮，页面切换，列表信息显示等功能。而且想要更改页面布局或者内容，直接在服务器端更改，更改后不用重新打包，打开APP就能直接更新。
综上所述，Web App有以下几个特点
* （1） 框架型APP应用的安装包小巧，只包含框架文件，而大量的UI元素、数据内容刚存放在服务器端；
* （2） APP用户每次都可以访问到实时的最新的服务器端数据；
* （3）APP用户无须频繁更新APP应用，与服务器端实现的是实时数据交互；
Web App虽然开发起来简单好用，但是随着需要用到的涉及手机的功能越来越多，Web App渐渐显得力不从心了，于是只好采用Native App开发。
# 二、Native App开发
因为是一个人开发，为了开发节省时间，我便开始在网上疯狂的找APP框架。一开始感觉怎么着也得是那种狂拽酷炫屌炸天的效果吧，运行了一个有一个，却发现很多都是徒有其表，为了效果把代码弄的是各种复杂，实用性一点都不强。只好退而求其次，找简单的。
终于找到一个合适的，又费了半天的功夫调试安装后却发现资料不全，能不能继续下去都是个问题。很想放弃然而已经花费了这么多的精力不能说放弃就放弃吧，于是就咬着牙把代码重新梳理整合了一下，总算把整体框架搭建好了，不过想要调用之前的脚本实现与服务器端交互，效果却不是很理想，只能重新构建服务器端逻辑了,造成的结果是生成的APP应用的安装包是之前的两倍多。

![Demo来自javaapk](http://upload-images.jianshu.io/upload_images/3845101-fccefbf6815bd686.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

综上所述，Native App有以下几个特点:
* （1）原生型APP应用的安装包相对较大，包含UI元素、数据内容、逻辑框架；
* （2）手机用户无法上网也可访问APP应用中以前下载的数据。
* （3）原生型的APP可以调用手机终端的硬件设备（语音、摄像头、短信、GPS、蓝牙、重力感应等）
# 三、Hybrid App开发
如你所见，Web APP无法调用手机终端的硬件设备，访问速度受手机终端上网的限制，而Native App虽然可以充分利用设备的特性，但是开发起来难度和代价却大。Hybrid App却综合了二者的特点。下面就一ionic的使用体验，谈谈Hybrid App开发体验。

![图片来自百度百科](http://upload-images.jianshu.io/upload_images/3845101-e2df5d40603413f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> ionic  是一个专注于用WEB开发技术，基于HTML5创建类似于手机平台原生应用的一个开发框架。绑定了AngularJS和Sass。这个框架的目的是从web的角度开发手机应用，基于PhoneGap的编译平台，可以实现编译成各个平台的应用程序。

首先安装ionic，确保电脑已经安装：[Node.js](http://nodejs.org/download/)（下载包），[JDK](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html?ssSourceSiteId=otncn#jdk-7u80-oth-JPR)（webstorm 运行环境），[Android SDK](https://developer.android.com/intl/zh-cn/sdk/index.html) (Android编译)，Android Studio。（具体教程请参照[ [轻松学习Ionic （一） 搭建开发环境，并创建工程](http://blog.csdn.net/zapzqc/article/details/41802453)](http://blog.csdn.net/zapzqc/article/details/41802453/)）

```
$ npm install -g ionic cordova
$ionic start iotApp tabs
cd iotApp
ionic platform add android 
```

![创建APP](http://upload-images.jianshu.io/upload_images/3845101-c0221aa4a97f12cd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然后，打开Android studio导入E:\Android\iotApp\platforms\android（这是本人电脑上的路径），导入后就可以编辑APP了。

![android studio](http://upload-images.jianshu.io/upload_images/3845101-20978b131c28215d.PNG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![APP效果](http://upload-images.jianshu.io/upload_images/3845101-ccbaa337e7c6342c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如你所见，仅仅修改HTML文件就可以直接在APP上显示了，当然还有很多功能等待大家探索，本人只是抛砖引玉。
# 四、总结
虽然水平有限，只是简单地带大家和我一起体验了三种开发方式，现在回到原题（不然会被骂标题党的），那么纯Native App开发模式还能走多久呢？个人觉得随着技术的更新迭代应该走不了多久，虽然最近“微软发招、苹果发飙:React Native遭躺枪”这样的新闻很火（PS.React Native也是一个移动应用开发框架），但是还是阻挡不了混合应用开发的脚步。

![图片来自Cordova官网](http://upload-images.jianshu.io/upload_images/3845101-ba537cf835c32098.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

上面这张图片可以看出，Hybrid App的原生体验相对于Web App，已经有了不小的进步，再加上其对JS与生俱来的支持，相信不久的将来其体验会越来越好。

以上仅属于个人实际体验和观点。最后以 Atwood定律结尾:
> 凡是能用JavaScript写出来的，最终都会用JavaScript写出来。