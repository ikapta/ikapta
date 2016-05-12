title: html5响应式开发
date: 2016-05-12 11:01:59
tags: [rem,viewport]
---

拜读腾讯的ISUX 文章 [web app变革之rem][1]，结合实际开发，造个简单的轮子。

## ViewPort篇
之前项目中的开发，一直是暴力的定死宽度640px或者750px;然后通过下面的一句代码,直接放在`head`中，设置最大放缩，某宝也有这样弄的。
```
<meta name="viewport" id="viewport" content="target-densitydpi=device-dpi,width=640, maximum-scale=0.5">
    <script>
        document.getElementById('viewport').setAttribute('content', 'target-densitydpi=device-dpi,width=640, maximum-scale=' + window.screen.width / 750);
    </script>
```
上面的代码是有问题的，在做渠道合作的时候，很多公司的 `webview`禁用了一些缩放，给我急的，那咋搞呢，这样，修改初始的放缩比例，然后禁用用户放缩：
```
   <meta name="viewport" id="viewport" content="target-densitydpi=device-dpi,initial-scale=1,width=640, minimum-scale=0.5,user-scalable=no">
    <script>
        document.getElementById('viewport').setAttribute('content', 'target-densitydpi=device-dpi,initial-scale=' + window.screen.width / 640+ ',width=640, minimum-scale=0.5,user-scalable=no');
    </script>

```
<!-- more -->

ok, 完美。 我在使用中也没遇到什么问题，开发也很方便，以后还会一直采用这种方法的。(在一开始的推荐文章中，作者说有时候图片会糊，也只是猜测，我们是640缩小页面又不是放大，图片质量好不会有问题)

## REM篇
参考开头的文章，以及结合一些实际例子，实际开发中的代码如下（上代码直观明了），以前都用bootstrap做响应式开发，现在直接改变 html的size就可以了
```
@charset "utf-8";
/*reset*/
*{
   padding:0;
   margin:0;
}
html{
   font-size: 62.5%;
}
@media screen and (min-width:321px) and (max-width:375px){html{font-size:11px}}
@media screen and (min-width:376px) and (max-width:414px){html{font-size:12px}}
@media screen and (min-width:415px){html{font-size:15px}}

body{min-width:320px;max-width: 640px;font-family:Helvetica;word-break:break-all;color: #4d4c4e;margin: 0 auto;}

.iconfont{font-size: 1.6rem;}
a{text-decoration: none; color:#4d4c4e; cursor: pointer; -webkit-tap-highlight-color:rgba(0,0,0,0); }
h1,h2,h3,h4,h5,h6{font-size: 1em; font-weight: normal;}
ul,ol,li{list-style: none;}
i,em{font-style: normal;}
input,button{font-size: 1em; font-family:Helvetica; outline: none;}
input[type="button"],button{border:none;}
select{font-family:Helvetica; appearance:none; -webkit-appearance:none;}
input[type="text"],input[type="password"],select,textarea{outline: none;}
img{max-width: 100%;}
table {border-collapse:collapse;border-spacing:0}
input, select{-webkit-appearance: none;appearance: none;outline: none;-webkit-tap-highlight-color: transparent;}
/* ============================================================
   flex：定义布局为盒模型
   flex-v：盒模型垂直布局
   flex-1：子元素占据剩余的空间
   flex-align-center：子元素垂直居中
   flex-pack-center：子元素水平居中
   flex-pack-justify：子元素两端对齐
   兼容性：ios 4+、android 2.3+、winphone8+
   ============================================================ */
.flex{display:-webkit-box;display:-webkit-flex;display:-ms-flexbox;display:flex;}
.flex-v{-webkit-box-orient:vertical;-webkit-flex-direction:column;-ms-flex-direction:column;flex-direction:column;}
.flex-1{-webkit-box-flex:1;-webkit-flex:1;-ms-flex:1;flex:1;}
.flex-align-center{-webkit-box-align:center;-webkit-align-items:center;-ms-flex-align:center;align-items:center;}
.flex-pack-center{-webkit-box-pack:center;-webkit-justify-content:center;-ms-flex-pack:center;justify-content:center;}
.flex-pack-justify{-webkit-box-pack:justify;-webkit-justify-content:space-between;-ms-flex-pack:justify;justify-content:space-between;}
.flex>*{display: block;}
```

  [1]: https://isux.tencent.com/web-app-rem.html