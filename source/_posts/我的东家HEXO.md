title: 我的东家HEXO
date: 2015-08-08 18:01:25
tags: [hexo,git]
---


------
无意间的一次玩弄`grunt`，发现了`hexo`，就花了点时间玩了玩,建了个博客。

## 安装过程
如果本机安装了node 忽略下面一段
### 安装git 和 node
这个就不介绍了，分别直接官网 [git][1] [node][5] 下载安装就好了，建议全局安装，不要逼格太高瞎折腾。其实也没啥关系，猿猿都爱折腾。
#### 错误解决
各种`npm`安装的插件对其操作命令过程中，如果系统提示没有这个命令，基本上不是需要update,就是没有全局安装，需要在系统路径下注册，即弄个环境变量。比如安装hexo`$ npm install -g hexo`发现`$ hexo -V`不好使，那就找到你安装hexo的根目录，copy路径，右键我的电脑<i class="fa fa-angle-right" />属性<i class="fa fa-angle-right" />高级系统设置<i class="fa fa-angle-right" /> 环境变量 <i class="fa fa-angle-right" /> 点开 **系统变量Path** 末尾添加类似路径C:\Program Files\nodejs\node_global。你就会发现你安装的插件都好用啦，比如`grunt hexo`
### 主要安装步骤
#### 安装hexo
利用`npm`命令就能全局安装hexo
```bush
 $ npm install hexo -g 
```
然后你可以`hexo -V`查看版本，ok(如果命令不好使，移步上面的错误解决)
#### 创建hexo文件夹
在自己需要建立文件夹的磁盘新建文件夹，然后敲下面的命令
```bush
  $ cd E:/myblog
  $ hexo init && npm install
```
先进入当前文件夹，然后两步一起走吧，初始化`hexo`,安装`npm`依赖，其实这就安装完了
#### 本地运行hexo
执行下面的命令
```bush
  hexo g && hexo s    //此处可以简写
```
没那么麻烦，`hexo generate` 编译文件，你会发现目录中多了`public`文件夹，里面就是生成的静态文件，然后`hexo server`运行server，没改配置文件的话，浏览器输入`http://localhost:4000/`,就能看到自己的网站了，内置了一篇hello world的文章。
#### 发布hexo
```bush
  hexo d    
```
执行上门的命令，前提打开`git Bash`,建议hexo相关的命令直接在`git bash`上敲,还要配置根目录下的`_config.yml`文件，
```
    deploy:
    type: git
    
        ## repository: git@gitcafe.com:yourname/myblog.git
        ## branch: gitcafe-pages
        
        ## repository: https://github.com/yourname/myblog.git
        ## branch: master
        
        repository: git@github.com:chanzig/yourname.github.io.git
        branch: master
```
写法有很多种，第一种我部署到了[gitcafe][4]上了,二三都是部署到github上，还可以合并写法，同时部署到各个仓库，得找一找格式忘了，目前我只需要`push`到一个仓库，用https:的需要在`deploy`的时候输入git账号密码，公钥密钥的ssh[\[参考移步\]][7]就行了，方便。
##### 发布大前提
`github pages` 得了解吧，你注册git的账号显示比如`steven`，然后你建立一个仓库名字叫`steven.github.io`,随便放一个静态页在`master`分支，就能访问这个地址了`steven.github.io`，只能拥有一个这样的仓库哦。
其他的仓库你可以建立`gh-pages`分支，访问`steven.github.io/仓库名称`。最好的代码托管的话，把`hexo deploy`的配置`brnach` 写成`gh-pages`然后`master`分支是整个工程文件，这样挺方便的，不然一开始那种还得建一个参考保存代码，我就是那么干的。
在`[gitcafe][5]`上我建立仓库，先弄个`gitcafe-pages`,把代码`delpoy`上去，然后再用`git` 切换到`master`分支，push工程文件，就好了，一个分支是我们的静态文件，一个分支是我们的项目文件，妥妥的。

### 我常用hexo命令
就是写博客以及发布保存：
```
hexo n "博客名称"  //新建文章，然后再用`markdown`打开写，不然乱码
hexo g && hexo s //编译并查看
hexo d //发布
<!-- more --> //截断文章显示 more>

git add .
git commit -m "new article"
git push -u origin master
```

### 关于本博客
借鉴于大兄弟Litten的 [Yilia][2]主题，然后做了很多细节修改。
>*  `Yilia`主题为什么用了`fontawesome`，然后阅读更多 用`more >>`标示，以及上一篇下一篇`>`这个表示,一个字懒，本来好好的主题给毁了；
* 还有我的天，左边栏给`fix`了，我加了一堆logo发现笔记本就看不见了，然后给改成`absolute`了；
* `tag`什么的都给放到隐藏的菜单了，好不方便的说，分类也给`false`了，反正改成`absolute`了，下拉的时候，左边的下方空间也大了，有时间给修改一下，把`widget`全给拿出来，或者下拉一定距离的时候，加个效果`Ding`[(like)](http://www.bootcss.com/p/stickup/)一下头像什么的；
* 代码高亮黑色背景类似`subline`，太晃眼了还是喜欢浅色的类似`github,segment`的`markdown`标记，还有行内代码也不太美观，有时间给修修；
* 自动文章目录导航也被去掉了，不喜欢，得自己动手加上去了，其实主题[Jacman][6]就挺好的，就是没用`jquery.lazy.load`,少了点特效，头部的大背景可以改精致一点，右边的`tag分类`看起来相当low,稍作修改，完全可以非常实用；
* 额外的，我把左边的二级标题换成[一言][3]了，纯属个人娱乐，每次刷新页面都会请求一次换一言；
* 还有一个问题，只有一篇文章的情况下，不显示`share按钮组` 和 `duoshuo评论` `!index`是不是歧义了，不细究了，再写一篇就没问题了
<pre>  
      <% if (!index){ %>
        <%- partial('post/nav') %>
      <% } %>

    <% if (!index && theme.share){ %>
    <%- partial('post/share') %>
    <% } %>
    
    <% if (!index && theme.duoshuo && post.comments){ %>
    <%- partial('post/duoshuo', {
        key: post.slug,
        title: post.title,
        url: config.url+url_for(post.path)
      }) %>
    <% } %>
</pre>



  [1]: https://git-scm.com/
  [2]: https://github.com/litten/hexo-theme-yilia
  [3]: http://hitokoto.us/
  [4]: http://gitcafe.com/
  [5]: http://nodejs.org/
  [6]: http://wuchong.me/jacman/
  [7]: https://help.github.com/articles/generating-ssh-keys/