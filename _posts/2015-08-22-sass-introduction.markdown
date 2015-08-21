---
layout: post
title:  "Sass 介绍"
date:   2015-08-22
categories: sass
---

本文讲解关于Sass的基本语法，不涉及如何编译到CSS，请自行搜索如何编译Sass。

## 嵌套
原生的CSS时不允许一个选择器嵌套到另外一个选择器，Sass可以提供这个特性。嵌套的好处可以不用写重复的选择器，而且如果改动祖先选择器名称，编译后的CSS选择器也会变动，这样避免改动祖先选择器需要进行多处修改。例如原生的CSS如下：

```css
.panel {
	border: 1px solid #ccc;
}
.panel .header {
	border-bottom: 1px solid #ccc;
}
.panel .footer {
	border-top: 1px solid #ccc;
}
```

上面的代码如果使用Sass的嵌套特性的话，代码可以改为：

```css
.panel {
	border: 1px solid #ccc;
	
	.header {
		border-bottom: 1px solid #ccc;
	}
	.footer {
		border-top: 1px solid #ccc;
	}
}
```
使用嵌套的话不仅仅结构更加清晰了，而且也更容易维护，学习的门槛也比较低，非常适合初学者使用。**需要注意的是嵌套尽量不要大于三层，不然会导致结构复杂，可读性差。**


## 变量
变量可以把常用的CSS值赋值给变量，如果CSS有多处使用这个CSS值的时候就可以用变量代替。语法如下:

```sass
$red: #fb012a;
	
.panel {
	border: 1px solid $red;
}

.card {
	border-bottom: 1px solid $red;
}
```
上面的例子如果使用原生CSS就需要在两个地方都使用`#fb012a`，当需要修改颜色时就不够灵活，使用变量后不管有几处使用了这种颜色，只需调用`$red`，编译后就可以修改CSS值了。
	
## Mixins
Mixins定义一组CSS规则，支持参数，方便在各处样式中复用，还避免命名一些没有语意的类名。编写一个特定规则的字体规则后，当某些元素符合规则的话就在相应的Class应用这个Mixins，例如下个的例子：

```sass
@mixin contextual-text() {
	.bg-success {
		font-family: Gill Sans Extrabold, sans-serif;
		font-size: 14px;
		padding: 0 10px;
	}
}

@include contextual-text;
```

定义Mixins使用指令`@mixin`，调用Mixins需要使用指令`@include`，下面来说明Mixins如何使用参数，继续上面的例子：

```sass
@mixin contextual-text($color) {
	.bg-success {
		font-family: Gill Sans Extrabold, sans-serif;
		font-size: 14px;
		padding: 0 10px;
		color: $color;
	}
}

@include contextual-text(#01fb4d);
```

## 总结

上文只是简单介绍了一些Sass的特性，但是也可以看出比原生CSS好用很多，对于项目的开发有极大的好处，极大提高开发效率。Sass社区也很活跃，有比较多的工具可以配合开发，例如[scss-lint](https://github.com/brigade/scss-lint)可检测你的代码质量，[sassdoc](http://sassdoc.com)可以从你的注释生成文档。最近Bootstrap 4也释出alpha版了，其中一个改变就是从Less迁移到Sass，从中也证明了Sass的流行。如果还没使用的朋友还是试试Sass吧！



	