title: gh-pages分支
date: 2015-08-19 21:36:34
tags: [gh-pages,git]
---

------
## gh-pages分支 ##
有必要记录一下这个分支了，好几天没用git，以及gitcafe，都快忘了这个分支了。



> 创建步骤

### 1.创建仓库
我们在git上创建一个仓库，名字当然就是自己的项目了`xx_demo`,其他的什么都不要做，什么都不要做，什么都不要做(重要的事情说三遍)(其实也没事，保持项目干净的说)，就算`readme`都不要添加。

<!-- more -->
### 2.克隆项目
然后我们就可以执行命令 `git clone xxx` 克隆项目到本地，此时我们的 `git bush` 命令终端显示的应该就是 `master`分支，但是 `git` 网站上并没有显示分支，这就对了。
### 3.建立gh-pages分支
直接终端上敲如下命令：

    git checkout --orphan gh-pages
这就建立并且切换到 `gh-pages` 分支了，然后我们去网站刷新看项目，出现 `gh-pages` 分支了。
### 4.建立这个分支干什么用
妈蛋，你不知道，也不会看到这篇小文子。
建立一个 `index.html` 的文件，执行命令提交上去：

    git add .
    git commit -m 'add file index.html' //引号后面是提交commend
    git push -u orgin gh-pages

然后我们就可以在项目的 `setting` 下面看到此项目已经发布到自己的网站二级目录字样：

     Your site is published at http://yourname.github.io/xxx_demo.
这个 `http://yourname.github.io` 是 `git` 为我们每个人默认的，自己去建一个仓库，名字就叫做 `yourname.github.io` 只能建立一个，放个静态页，访问这个网址，你就能看到自己的网站了，然后我们建立其他的项目，同理只要建立一个**干净的**分支 `gh-pages`，就可以访问了`http://yourname.github.io/xxx_project`.这个是永久的网址，放一些demo在上面完全可以，当然如果你的把 `git` 的这个网址解析成自己的域名，当然会重定向到自己的域名的，试试就知道了。