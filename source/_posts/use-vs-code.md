title: use vs code
date: 2016-02-29 23:22:12
tags: [tools,vscode]
---

电脑上一直装了 `subline text3` \ `webStorm` \ `vs code`.
前两款需要密钥，对咱们来说都不是事情...而且 `subline text3` 安装已经有写过一篇大概的介绍 [user-subline-text3][1]，本文主要是自己暂时用 vscode 的一些常用的插件和命令，有待更新。
<!-- more -->
说真的，`subline`快是绝对的，可以试试打开超大数据的`txt`文件的时候，`vs code`绝对反应慢很多，`subline`的分屏实在是太陋了。`webStorm`强大到我都怕，另外国内现在的`Hbuilder`做的也很完善了。但是一直很喜欢这个干净整洁的界面，就本身来说也是个 `vs` 使用者，所以还是转投`vs code`
### 插件
插件的安装 类似 `subline` ;快捷键`ctrl +shift +p`或者`F1` 输入 `ext`， 点提示`install extention`,然后模糊搜索插件名字。
[官网][2] 的插件种类不要太详细！
tips:**安装了插件后，更多快捷键，请在`F1`命令窗口中搜索**

 1. js-css-HTML Formatter :代码格式化工具，快捷键`alt+shift+f`;

 2. [Beatity][5] :同样的代码格式化工具，但是没有快捷键，每次都是在控制台中输入 `Beautity`
    命令，和上面格式化的效果有点不一样，看个人喜好，使用中暂时发现他的`css`格式化更完美一点，并列的逗号写法会换行显示;以及html文件格式化更准确

 4. Can I Use;

 5. html preview : 快捷键 `ctrl+shit+H`

 6. Markdown语法预览快捷键 ：`ctrl +shift+v` (toggle)

 7. 主题切换：安装了主题文件后，`F1`中输入 `theme` 选择`color theme`
    默认的主题和安装的都在了，上下键预览,其实默认的也很棒

 8. `Ctrl+space` 代码提示
 9.  分屏：`ctrl+2`-两个页，`ctrl+1`一个页
10. 分完屏幕有时候就需要 `ctrl+B` toggle左边的导航树
11. 关闭完左边的可视导航，又得打开其他的文件，不用开启导航树：`ctrl+p` 输入大概的文件名确定ok
12. `npm`: 各种命令都支持
13. `angualr/ react/ jsx/ gulp ...`
14. f5调试js 还有执行task命令
15. ` ctrl+` `显示自带命令提示符，非常好用
16. ` ctrl+d `同时匹配一样的文字，可以同时修改。另外搜索一样文字的时候，按下 `ctrl+enter` 可以快速用光标定位所有一致结果，同时修改

17. mac terminal 一键打开项目：需要 f1 输入 ` install ` 找到install code in path. 然后就可以使用 `code .` 命令

语法提示的就在官网上找吧，不要太方便，就是没找到好用的`sass`提示，比如我调用了一个文件中的 `@mixin`或者变量，然后不能很好的提示，或者定位到它，这个非常不爽[`web storm`就可以]。

**[基于typescript或者javascript 完全可以自己动手写一个扩展][4]**
  [1]: /2015/08/09/use-subline-text3/
  [2]: https://marketplace.visualstudio.com/#VSCode
  [3]: https://marketplace.visualstudio.com/items?itemName=Zignd.html-css-class-completion
  [4]: https://code.visualstudio.com/docs/extensions/example-hello-world
  [5]: https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify
