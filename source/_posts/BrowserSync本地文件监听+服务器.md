title: BrowserSync本地文件监听+服务器
date: 2016-03-07 01:38:37
tags: [borwser-sync,glup]
---
这是一款非常棒的基于`node`的插件，可以监听文件和当做本地服务器。
###应用场合 -- 手机调试访问（同一局域网）

> 想象一下，我做了一个简单的只有 `html` 的微信页面，想用手机看效果，怎么办？

 - 要么在本地的`iis`上建起来，然后还得关闭防火墙什么的，才能打开漂亮的页面（or 扔到线上服务器）。
 - 或者百度搜一下本地微型服务器，使用别人写的简单的 `windows` 有个叫 [小苹果][1] 的程序，安装一下才能访问。这个有个好处，集成了我们熟悉的 **weinre远程调试**！良心之作。
 - 我还想去用`gulp`自动化一下当前项目，好想法。想想接下来的步骤是 初始化/配置config/安装依赖/ 配置`gulp`自动刷新服务器 [gulp-livereload][2] or [gulp-connect][3] or [browser-sync][4],当然`connect / borwser-sync`要好用的多。

> ！都不是我想要的，我要的是 全局的 **borwser-sync** 


----------


全局安装

    npm install -g browser-sync 

安装完毕，直接cmd进入项目目录,执行下面的命令：

    browser-sync start --server 

结果，然后就可以访问了：

![访问路径显示][5]

其中`UI`是插件自带的后台，功能很强大，同样集成了我们熟悉的 **weinre远程调试**，哈哈良心。以后每次想手机看电脑上的静态页面，只要在项目目录下执行`browser-sync start --server `就ok了。

此处只介绍 `browser-sync` 如何运行在本地，然后通过其他设备访问本地文件。其他各种命令移步非常详细的 
[官方中文文档][6]


  [1]: http://pan.baidu.com/s/1i4ju7GT
  [2]: https://github.com/vohof/gulp-livereload
  [3]: https://github.com/AveVlad/gulp-connect
  [4]: https://github.com/BrowserSync/browser-sync
  [5]: http://7xl7z0.com1.z0.glb.clouddn.com/browser-sync.png
  [6]: http://www.browsersync.cn/docs/command-line/
