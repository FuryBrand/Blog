---
layout:     post
title:      "MacOS-一些使用小技巧"
date:       2020-11-02 18:10:00
author:     "Steve"
header-img: "img/home-bg.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 技术相关
    - macOS
---


> 从我大Windows切换到MacOS之后，会有诸多不太习惯的地方，这里做一个记录

## 设备信息

- 型号：MacBook Pro (16-inch, 2019)
- 系统版本：macOS Catalina Version:10.15.7（19H2）

## 在Finder中通过VSCode打开文件夹

其实就是Windows上的`右键->Open With Code`功能。可以直接参考这个[文章](https://www.cnblogs.com/yangisme/p/12297317.html)，虽然看起来OS的版本有点老，但是整体没啥变化。我实在懒得切换系统语言了。。。。（作为一个会中英日三门语言的大叔，最近在习惯日文系统😜）

**Launchpad -> Automator -> 快速操作**

![01]({{ site.url }}assets/2020/2020-11-02-make-mac-better/01.heic)

**按下图进行配置 -> cmd s -> 输入“Open_With_Code”**

![02]({{ site.url }}assets/2020/2020-11-02-make-mac-better/02.heic)

```shell
for f in "$@"
do
	open -a "Visual Studio Code" "$f"
done
```

**在Finder中右击文件夹就可以找到刚刚创建的快速操作了**

![03]({{ site.url }}assets/2020/2020-11-02-make-mac-better/03.heic)

## 图片的格式及画质转换

稍微有点理解macOS对于媒体工作者的强大之处了。Windows上对于图片转换一直没有找到很合适的软件，但是macOS的原生功能就很强大了，可以选择格式，还可以选择质量，很强。

**打开图片 -> 文件 -> 导出**

![04]({{ site.url }}assets/2020/2020-11-02-make-mac-better/04.heic)
![05]({{ site.url }}assets/2020/2020-11-02-make-mac-better/05.heic)

## 更新日志
- 2020年11月02日：初稿。