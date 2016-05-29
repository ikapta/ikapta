title: 移动viewport
date: 2016-05-29 13:08:33
tags: [viewport,移动h5]
---

之前在公司一直是用 `bootstrap`,然后我们技术部门的权利始终是大于设计师的，所以我们对着设计稿能做出什么样子，他们都不会说话，哈哈。可惜现在的处境是对着设计稿一边量尺寸一边写，像素根本不能差太多，不然设计师会说你这还原度太差了吧！fuck,想当年轮到你来说老子。
老实说，用`bootstrap`的时候，对着图片写，与设计差几乎看不出来，而且通用适配 `pc ipad mobile` 。期间也做过一些公司外的h5，没用boot，用的百分比。也一样写的很好。但是来到新的公司后，突然还是有一些不知所措，面对h5的适配。、

目前的项目所有页面中这样写的：
```
<meta name="viewport" content="target-densitydpi=device-dpi,width=640,user-scalable=no" />
document.getElementById('viewport').setAttribute('content', 'target-densitydpi=device-dpi,initial-scale=' + window.screen.width / 640+ ',width=640,user-scalable=no'); 
```
页面宽度定死640,所有终端适配。

但是，渠道推广部们接了很多合作商，我们的h5放在他们的 `webview`，中就爆炸了，上面的js完全不好使。
后来建议使用传说中的 **完美屏幕**
```
<meta name="viewport" content="initial-scale=1.0,width=device-width,user-scalable=0,maximum-scale=1.0"/>

//我的使用方法是直接设置页面宽度640
<meta name="viewport" content="width=640,user-scalable=no" />
//或者
<meta name="viewport" content="target-densitydpi=device-dpi,width=640,user-scalable=no" />

```
下面是网易的用法，也是640宽度，js适配：
```
(function (window) {
    var viewport = document.documentElement.querySelector('meta[name="viewport"]');
    var initWidth = 640;
    var a = initWidth;
    var b = window.innerWidth || a
      , c = window.outerHeight || b
      , d = window.screen.width || b
      , e = window.screen.availWidth || b
      , g = window.innerHeight || a
      , h = window.outerHeight || g
      , i = window.screen.height || g
      , j = window.screen.availHeight || g
      , k = Math.min(b, c, d, e, g, h, i, j)
      , L = k / a
      , m = window.devicePixelRatio
      , L = Math.min(L, m);
    var device = window.navigator.userAgent;
    if (device.match(/Android/gi)) {
      window.device = 'android';
      document.body.className += ' android';
      viewport.setAttribute('content',
        'width=' + a + ' initial-scale=' + L + ' maximum-scale=' + L + ' user-scalable=no'
      )
    } else if (device.match(/iPhone|iPad/gi)) {
      window.device = 'ios';
      viewport.setAttribute('content',
        'width=' + a + ' user-scalable=no'
      ) 
    }
    // 判断微信
    if (device.match(/MicroMessenger/gi)){
      document.body.className += ' weixin';
    }
  })(window)
```

上面都是，定死宽度，然后关于viewport设置的，开发方便，不用再写一堆媒体查询。
参考文章：
[手机百度移动适配切图解决方案介绍。][1]
[移动端适配方案(上) ][2]
[移动端适配方案(下) ][3]


[1]: http://js8.in/2015/12/12/%E6%89%8B%E6%9C%BA%E7%99%BE%E5%BA%A6%E7%A7%BB%E5%8A%A8%E9%80%82%E9%85%8D%E5%88%87%E5%9B%BE%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88%E4%BB%8B%E7%BB%8D/
[2]: https://github.com/riskers/blog/issues/17
[2]: https://github.com/riskers/blog/issues/18

