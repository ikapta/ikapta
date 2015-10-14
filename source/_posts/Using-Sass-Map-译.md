title: Using Sass Map(译)
date: 2015-10-15 01:21:00
tags: [译,Sass,Map]
---
在Sass的第三个版本中引入了一个新的数据类型`map`,虽然你不熟悉这个名字，但其实我们已经频繁的在其他语言中使用`maps`，例如处理`associative arrays`或者`hashed`。简单的说：一个`Sass Map`就是一个数组的键值对 `key to values`。
尽管现在我们还是不太清楚为什么要在`CSS`[Sass is CSS]中使用`maps`，没关系，这里会有你想要的。这篇文章并不是详尽无疑，但你可以轻松的去发现、分享和使用这些案例。

## 语法 for Sass Maps ##
在进一步讨论之前，让我们每一个人站在同一个起跑线上。
`Sass`地图使用括号作为外部的分隔符，冒号映射键和值，逗号来分割键/值对。下面就是一个规范的`Sass Map`
```css
    $map:(
        key: value,
        other-key: value
    )
```
看了上面，接下来有几件事你应该知道：
<!-- more -->
 - 我们有很多`functions`可以让你轻松的处理这些`maps`[传送门][1]
 - 在`Map`上的最后一个键/值对,可以选择跟一个逗号
 - 键必须唯一
 - 键和值可以是任意的`Sass`类型，例如`lists` 或者 `maps`

再强调一次，`keys`不一定就是`string`,可以是任何东西：`null`或者`maps`。几周前，我和Chris Eppstein, Micah Godbolt, Jackie Balzer有个激烈讨论。[传送门][2]就是在`JavaScript`中有一种场合，我觉得很不满意，它不使用字符串作为`hash key`。但是在Sass中，没有什么不可能。

Okay,现在我们可以出发了。

## 项目配置 Project Configuration ##
让我们从一个简单的使用场合开始。`Maps`很容易在项目中配置使用。很简单：把键值对匹配上，然后我们就可以在项目中的任何地方通过 `map-get($map,$key)` 这个方法引用。
其实我已经在我的这篇文章[在Sass中管理响应式breakpoint][3]中使用过这个方法，下面是一个简单的例子：
```css
// _config.scss
$breakpoints: (
  small: 767px,
  medium: 992px,
  large: 1200px
);

// _mixins.scss
@mixin respond-to($breakpoint) { 
  @if map-has-key($breakpoints, $breakpoint) {
    @media (min-width: #{map-get($breakpoints, $breakpoint)}) {
      @content;
    }
  }

  @else {
    @warn "Unfortunately, no value could be retrieved from `#{$breakpoint}`. "
        + "Please make sure it is defined in `$breakpoints` map.";
  }
}

// _component.scss
.element {
  color: hotpink;

  @include respond-to(small) {
    color: tomato;
  }
}
```
编译结果：
```css
.element {
  color: hotpink;
}

@media (min-width: 767px) {
  .element {
    color: tomato;
  }
}
```
是不是很酷。另一个非常棒的案例是对 `color` 的处理。项目中，我们经常为 `color` 用 `variables` 区分开是很nice的，但是当你有数十个变量值的时候，会变的很凌乱。所以为主题 `color` 制作一个 `map`, 再拆分出一些 `sub-maps`，这应该是一个不错的idea。
```
// _config.scss
$colors: (
  sexy: #FA6ACC,
  glamour: #F02A52,
  sky: #09A6E4
);

// _component.scss
.element {
  background-color: map-get($colors, sky);
}
```
最终，你可能会厌倦一遍又一遍的通过`map-get($colors,...)`去取值。没关系，我们可以通过一个简单的`helper function`来缓解你的痛苦：
```
// _functions.scss
@function color($key) {
  @if map-has-key($colors, $key) {
    @return map-get($colors, $key);
  }

  @warn "Unknown `#{$key}` in $colors.";
  @return null;
}

// _component.scss
.element {
  background-color: color(sky); // #09A6E4
}
```
在这个话题，我觉得你可能有兴趣去读一读Erskine Design写的 [这篇文章][4]。

让我们看一下最后一个`maps`项目配置使用案例 *z-index layers*。我觉得这个写法配置第一次出现在Chiris Coyier 的文章中  [Handling z-index][5]。你是不是经常这样干`z-index:999999999`？好的，现在一切都结束了。
```
// _config.scss
$z-layers: (
  bottomless-pit: -9999,
  default: 1,
  dropdown: 3000,
  overlay: 4000
  modal: 4001
);

// _functions.scss
@function z($key) {
  @if map-has-key($z-layers, $key) {
    @return map-get($z-layers, $key);
  }

  @warn "Unknown `#{$key}` in $z-layers.";
  @return null;
}

// _component.scss
.overlay {
  z-index: z(overlay);
}

.element {
  z-index: (z(default) + 1);
}
```

鉴于我们搞砸了`z-index`，我觉得把把所有的`index`放到一个简单的`map`中，并且始终坚持使用维护他们。以后你就会知道你的程序中有多少`layer`层在使用，而且很清楚的知道程序发生了什么，同时很容易清晰的去`debug`。

## 模块配置 Module Configuration ##
我们必须始终坚持组织配置，才能让我们进一步深入应用程序管理，解决模块/组件配置。我已经写了一篇文章[Bringing Configuration Objects To Sass][6] 使用`Sass Maps`来管理配置对象，并且它为什么值得去挖掘值得这样做。概念验证：
```
// _mixins.scss
@mixin module($options: ()) {
  $configuration: map-merge((
    color: grey,
    duration: 0s,
    border: null
  ), $options);

  color: map-get($configuration, color);
  transition: map-get($configuration, duration);
  border: map-get($configuration, border);
}

// _component.scss
.element {
  @include module((
    color: pink,
    duration: .15s
  ));
}
```
上面这种方案有一个问题，它使得 `mixin signature ` 非常通用。在生活中，一个signature签名代表了一个人。当我们看一个  `function/mixin` 签名的时候，我们必须去看哪些参数被执行了，执行了什么，生成了什么`css`。这种方式不对，因为我们必须去看这个 `mixin` 默认的参数操作，才知道发生了什么。

为了解决这个问题，我们定义一个详细的`signature`(常规的多个参数)的 `mixin` 然后只包含一个配置图 `configuration map`，让我们重写之前的例子。
```
// _mixins.scss
@mixin module($color: grey, $duration: 0s, $border: null) {
  color: $color;
  transition: $duration;
  border: $border;
}

// _component.scss
.element {
  @include module((
    duration: .15s,
    color: pink
  )...);
}
```
在这种情况下, `…` 扩展映射的值,这样每一对都被视为一个关键字参数。不仅使`mixin signature` 更加明确，也为之前`map-merging`的 `mixin's core` 留出了位置。
因此这样你可以使用`Sass Maps`去配置包含多个参数的`mixin`,如果我没弄错的话，`Pathon` 是为数不多的几个(著名)的语言允许你调用一个含有多个参数的二维数组的函数。我想说的是，`Sass` 也可以做到到。

## 解决冗余 Repetitive Stuff ##
到现在,我们仅仅使用 `map` 获得到一个特定的键和它相关联的值。另一个功能是避免写重复的东西。`CSS` 是一种非常**WET**(write everything twice)的语言,代码重复很普遍。这就需要一个循环和一个`list/map` 来帮你这么干，帮助你解决代码**DRY**(Don’t Repeat Yourself)。
来看着下面的 `icon fonts`，通常都是在`:before`伪类之前放一个对应的名字，例如：
```
.fa-glass:before {
  content: "\f000";
}
.fa-music:before {
  content: "\f001";
}
.fa-search:before {
  content: "\f002";
}
.fa-envelope-o:before {
  content: "\f003";
}
.fa-heart:before {
  content: "\f004";
}

/* ... */
```
Wow.太重复了，太多**WET**，我们为什么不直接把类名映射到字符编码？
```
$icons: (
  glass: "\f000",
  music: "\f001",
  search: "\f002",
  envelope-o: "\f003",
  heart: "\f004"
);

@each $name, $icon in $icons {
  .fa-#{$name}:before {
    content: $icon;
  }
}
```
很好，不是吗？尤其是当你有很多很多的图标的字体的时候就该这么做。如果你想了解更多，`Frédéric Perrin `通过这种非常棒的方法创建了 [a cool little demo][7] 在 `CodePen` 上；另外[一篇文章][8]以同样的方式来处理背景图片。
## CSS 存储（Dump） ##
如果我没记错的话，`Micah Godbolt` 写的[这篇文章][9]是第一次通过一个案例介绍这个`CSS Dump`。接下来，我们通过使用`Sass Map`作为一个`CSS list`的声明。你看，你看,`Sass`维护者尽力坚持尽可能接近官方的`CSS`语法在实现新功能。这就是为什么他们决定用 `()`括 号作为`list/maps(在媒体查询中使用)`，冒号作为映射操作（在任何声明中使用）。

因为`Sass maps`看起来像一个 `css list`规则，你可能写一个 `mixin` 去存储一个`Sass Map`的内容：
```
// _mixins.scss
@mixin print($declarations) {
  @each $property, $value in $declarations {
    #{$property}: $value
  }
}

// _component.scss
.element {
  @include print((
    margin: 0 auto,
    max-width: 50%,
    overflow: hidden
  ));
}
```
现在你有可能会去想，为什么要这样？为什么不直接写`css` 而是通过一个`mixin`?这个和上下文有关，当处理一个`module or something`,通常使用地图存储几个变量，然后组件应该怎样显示。例如：
```
// _component.scss
$configuration: (
  padding: 1em,
  margin: 0 1em,
  color: grey
);

.element {
  color: map-get($configuration, color);
  padding: map-get($configuration, padding);
  margin: map-get($configuration, margin);

  &::before {
    background-color: map-get($configuration, color);
  }
}
```
没必要每次获通过`key`去获取`value`,我们应该简单的写个 `css() mixin` 来打印输出`map`:
```
// _component.scss
.element {
  @include print($configuration);

  &::before {
    background-color: map-get($configuration, color);
  }
}
```
编译结果：
```
.element {
  padding: 1em;
  margin: 0 1em;
  color: grey;
}

.element::before {
  background-color: grey;
}
```
这足以解释`sass map`,但一切并没有结束，还有更多的东西值得我们去挖掘。

## Final Thoughts ##
如您所见,Sass地图特性是一个强大的工具。它不仅使代码更加结构化,同时也可以帮助你避免一些代码膨胀和重复。你呢,你怎样使用`Sass Map`?


  [1]: http://sass-lang.com/documentation/Sass/Script/Functions.html#map-functions
  [2]: http://www.sitepoint.com/using-sass-maps/
  [3]: http://www.sitepoint.com/managing-responsive-breakpoints-sass/
  [4]: http://erskinedesign.com/blog/friendlier-colour-names-sass-maps/
  [5]: http://css-tricks.com/handling-z-index/
  [6]: http://hugogiraudel.com/2014/05/05/bringing-configuration-objects-to-sass/
  [7]: http://codepen.io/blustemy/pen/mifBg?editors=010
  [8]: https://robots.thoughtbot.com/removing-sass-duplication
  [9]: http://www.phase2technology.com/blog/exploring-maps-in-sass-3-3/