---
layout: post
title:  "Linux-浅谈Nginx的反向代理 即http请求经历了什么😀（未完）"
date:   2019-03-12 23:20:25 +0800
categories: jekyll update
---

这两天解决了几个环境的问题，觉得自己对于http请求在请求过程中是如何流传的，以及Nginx的反向代理功能有了更深的认识。

但是只是有一个大体的认识还“不以雄远国”（哈哈哈，装完逼就跑真刺激。最近是真的中了易中天老师《品三国》的毒）。所以英文标题为`small talk`，就是聊聊自己的看法，大家看看就好，没准会有各种纰漏呢ε=ε=ε=┏(゜ロ゜;)┛

## 一个http请求的一生

标题开的有点大，细节东西太多了，不过如果是Linux+Nginx+Tomcat的话，大体上符合我下面的图样子。

这里我要说明一下，这个图是按照俺们公司的测试环境绘制的，实际线上的话，nginx可能是单独的一台服务器，不止实现反向代理，还有缓存负载均衡等功能。而相应的tomcat服务也会部署到不同的服务器上。甚至catA会同时存在数个为了应付高并发的情况。

![http请求的一生]({{ site.url }}assets/2019-03-12-Linux-Nginx-Tomcat-small-talk/图片1.png)

### 为什么可以通过域名访问到服务器？

首先我们看第一步`①我要访问catA.xixi.com`。为啥在浏览器输入了`catA.xixi.com`之后，浏览器就会把请求发送到指定的服务器上呢？

测试环境的话，就要归功于hosts的配置了，一般都用[SwitchHosts](https://github.com/oldj/SwitchHosts)来进行配置，配置好之后当浏览器要访问的时候会先去配置中看下是否有有指定的服务器ip地址，如果有的话，请求就直接打给这个服务器了。

那么为啥我访问`www.jd.com`买东西的时候不用配置hosts呢？难道我们每个人的PC都记住了全世界网站服务器的ip地址吗？

当然不是啦，这里要说一下，其实互联网在发展之初是没有`域名`这个概念的，两台计算机在通信的时候都是通过ip地址去找对方的，但是这也太麻烦了吧，对人类很不友好，记不住啊。所以`域名`以及`DNS(Domain Name Server，域名服务器)`也就应运而生了。当我们让浏览器访问`www.jd.com`的时候，计算机会去DNS上查找这个域名对应的ip地址，然后发请求发出去。不过由于测试环境的域名不会注册到DNS上，所以就要通过配置hosts来进行访问了。

### Nginx是如何接到请求的？又是怎么找到catA的？

我们都知道80端口是http的默认请求端口，所以Nginx启动后就会默认监听这个端口。当请求数据抵达服务器时，Nginx就会接到请求。而Nginx又如何找到在第二步`②catA帮忙处理一下`的呢，这就要看Nginx的配置文件了。我们假定Nginx服务的路径是这样的`/services/Nginx/conf/domains/`，那么在该文件夹下应该会看到这些文件。

```
catA.xixi.com
catB.xixi.com
catC.xixi.com
```

看一下Nginx配置文件的内容：

```
配置文件
```

从中我们可以看到，当请求的地址是`catA.xixi.com`的时候，Nginx会自动将根据请求地址的不同进行转发