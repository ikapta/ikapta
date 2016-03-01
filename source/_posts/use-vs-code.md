title: use vs code
date: 2016-02-29 23:22:12
tags: [tools,vscode]
---

电脑上一直装了 `subline text3` \ `webStorm` \ `vs code`.
前两款需要密钥，对咱们来说都不是事情...而且 `subline text3` 安装已经有写过一篇大概的介绍 [user-subline-text3][1]，本文主要讲vs code 的一些自己常用的插件和命令，有待更新。
<!-- more -->
说真的，`subline`快是绝对的，可以试试打开超大数据的`txt`文件的时候，`vs code`绝对反应慢很多，`subline`的分屏实在是太陋了。`webStorm`强大到我都怕，另外国内现在的`Hbuilder`做的也很完善了。但是一直很喜欢这个干净整洁的界面，就本身来说也是个 `vs` 使用者，所以还是转投`vs code`
### 插件
插件的安装 类似 `subline` ;快捷键`ctrl +shift +p`或者`F1` 输入 `ext`， 点提示`install extention`,然后模糊搜索插件名字。
[官网][2] 的插件种类不要太详细！
tips:**安装了插件后，更多快捷键，请在`F1`命令窗口中搜索**
> js-css-HTML Formatter :代码格式化工具，快捷键（alt+shift+f）;
> [Beatity][5] :同样的代码格式化工具，但是没有快捷键，每次都是在控制台中输入 `Beautity` 命令，和上面格式化的效果有点不一样，看个人喜好，暂时发现他的`css`格式化更完美一点，并列的逗号写法会换行显示
> [HTML CSS Class Completion][3]: 写html的时候可以快速的提示 class-name;
> Can I Use;
> html preview : 快捷键 （ctrl+shit+H）
> Markdown语法预览快捷键 ：ctrl +shift+v (toggle)
> 主题切换：安装了主题文件后，`F1`中输入 `theme` 选择`color theme` 默认的主题和安装的都在了，上下键预览,其实默认的也很棒



语法提示的就在官网上找吧，不要太方便，尤其支持 `react` \ `angular`语法，就是没找到好用的`sass`提示，比如我调用了一个文件中的 `@mixin`或者变量，然后不能很好的提示，或者定位到它，这个非常不爽[`web storm`就可以]。

**[基于typescript或者javascript 完全可以自己动手写一个扩展][4]**
  [1]: /2015/08/09/use-subline-text3/
  [2]: https://marketplace.visualstudio.com/#VSCode
  [3]: https://marketplace.visualstudio.com/items?itemName=Zignd.html-css-class-completion
  [4]: https://code.visualstudio.com/docs/extensions/example-hello-world
  [5]: https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify