---
layout:     post
title:      "HTTP代理调试工具——Fiddler简易实践"
date:       2020-07-30 12:47:00
author:     "Steve"
header-img: "img/home-bg.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Fiddler
    - HTTP
    - 技术相关
---


> 最近测试了一些移动端的东西，Fiddler用的突然多了起来，做下记录吧。

## 简介

摘自官网上简介`Fiddler Everywhere: The Web Debugging Proxy Tool Loved by Users Just Got Better. Log all HTTP(S) traffic between your computer and the Internet. Inspect traffic, set breakpoints, and fiddle with request/response. `说人话就是Fiddler可以记录PC和外部进行的所有HTTP通信，并且可以断点、发起request、控制response。总之就是对付HTTP的高端利器。目前对于HTTPS的接触不多，以后研究了再更新吧。

## 用法

我目前用到的场景不太复杂。版本目前使用的是官网提供的最新的`Fiddler Everywhere`。界面摩登了许多，但是少了些不常用的功能（TextWizard啥的）？使用了账号的方式登录，免费账号提供了一定数量的信息同步能力。

#### 1.抓PC的包

![初始状态]({{ site.url }}assets/2020/2020-07-30-fiddler-simple-guide/20-08-05_20-45-32.png)

打开软件之后，激活`Live Traffic`为`Capturing`便可以开始抓取电脑上所有网络的请求了。可以使用Filters去筛选Request Headers、Response Headers（对比经典版发现貌似少了查找功能😓）。

#### 2.抓手机的包

抓取手机的一些请求需要开启Fiddler的代理功能。然后手机和电脑连接在相同的路由器下，或者手机连接电脑的自建热点。

![配置信息]({{ site.url }}assets/2020/2020-07-30-fiddler-simple-guide/20-08-05_21-14-26.jpg)

上面是我的配置信息（Windows10开启热点后，手机进行连接）。ios和安卓类似，都是在WLAN中进行代理的设置。注意，设置了代理之后若Fiddler不启动，手机是无法正常上网的。

另外由于是“借壳上市”，所以请求“应该”是借用Fiddler使用当前环境进行的。**故PC端配置的Hosts是可以生效的。** 

#### 3.调试被调http接口

其实就是将抓到的请求放到`Composer`中去执行，可以手动改变一些请求的参数。`Fiddler Everywhere`的`Composer`和`Postman`很像，之前遇到类似的情况是浏览器抓请求，然后粘贴...粘贴...到`Postman`中去执行的。现在可以直接EXECUTE了。

![Composer]({{ site.url }}assets/2020/2020-07-30-fiddler-simple-guide/20-08-05_21-49-12.png)

#### 4.mock被调http接口

![AutoResponder]({{ site.url }}assets/2020/2020-07-30-fiddler-simple-guide/20-08-05_22-35-56.png)

Fiddler可以阻断请求，然后按照我们的预想进行返回，这个功能用的并不多，试了下。需要激活`Live Traffic`为`Capturing`同时激活`Auto Responder`才能生效，具体的规则配置方式还是参考官方的文档吧。[AutoResponder的官方手册](https://docs.telerik.com/fiddler-everywhere/user-guide/live-traffic/autoresponder#match-rules)


## 更新日志
- 2020年7月30日：初稿。

## 友链
- [官网](https://www.telerik.com/fiddler)
- [官方手册](http://wiremock.org/docs/)