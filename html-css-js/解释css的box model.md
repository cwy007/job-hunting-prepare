
# 盒模型，可以简单解释为：盒模型用来描述元素�所占据的空间。

boxdim.png
有两种盒模型：W3C盒模型(标准盒模型)和IE盒模型
这两种盒模型，主要区别是在解释元素的width和height属性上。
W3C盒模型认为：元素的with和height属性仅仅指content area。
IE盒模型认为：元素的with和height属性 由content area + padding + border组成。

所以：
W3C盒模型 元素的总共宽和高：
```
Total element width = width + left padding + right padding + left border + right border + left margin + right margin
Total element height = height + top padding + bottom padding + top border + bottom border + top margin + bottom margin
```

# �IE盒模型 元素的总共宽和高：

```
Total element width = left margin + width + right margin
Total element height = +top margin + height + bottom margin
```
在IE5.5和以及更早的IE版本中，IE都采用了IE盒模型，从IE6开始提供了一种IE使用W3C盒模型的方式：在html中声明Doctype。但是，IE6默认的仍旧是IE盒模型(quirks model模式)。

其实， IE盒模型更符合人们的思考方式，所以W3C在css3.0中加入了box-sizing，用来修改css box model，默认值是content-box(W3C的盒子)，border-box值设置IE盒子。

# �Tips：

* 以前由于思考习惯和看到设计切的图以及在浏览器中看到实际的html页面等原因，错误的将元素的width、height属性当做元素的实际宽、高，经过这段时间的研究，终于对这个问题有了新的认识。由于margin始终是transparent(透明)，更容易在计算元素宽高时将其忽略掉。

* background-color
设置元素的背景色：包括content padding border，不包括margin
margin背景色始终为transparent

* 外边距合并(塌陷)(collapsing margin)

* css3 中内容大小
如果box-sizing是默认值(content-box)，width, min-width, max-width
, height, min-height与 max-height控制内容大小。


链接：https://www.jianshu.com/p/2e787c6d8ede


# 概念
在一个html文档中，每个元素都被表示为一个矩形的的盒子。这每一个矩形的盒子被描述为盒模型(CSS Box Model)。并且这个模型描述了元素所占空间的内容。

# 组成

一般情况下，一个盒子是由以下部分组成

```
width = content-width + padding-left + padding-right + border-left-width + border-right-width

height = content-height + padding-top + padding-bottom + border-top-width + border-bottom-width

```
margin 指外边距，主要是为了分隔与当前元素之外的元素的距离。由于盒子之间共享外边距，有时会出现外边距`合并/塌陷`的情况。例如下面一段代码。

```CSS
.box {
  width: 200px;
  height: 200px;
  background-color: green;
  border: 5px solid red;
  padding: 20px;
  margin: 40px;
}
.box2 {
  margin-top: 60px;
}
```

box1 的 bottom 距离 box2 的 top 并不会有 40px+60px=100px 的距离，而是有 60px 的距离。

```html
<div class="box box1">
  <img src="https://beimg.oss-cn-beijing.aliyuncs.com/favicon.png!ace" />
</div>
<div class="box box2">
  <img src="https://beimg.oss-cn-beijing.aliyuncs.com/favicon.png!ace" />
</div>
```

# box-sizing 下的计算
box-sizing用于更改浏览器默认的盒模型计算方式。可谓是开发者编辑UI的福音。他解决了无数多关于占位、溢出、宽高计算、居中计算的问题。

以下是他的两个关键属性：

```
box-sizing: content-box; 默认值，盒子占有的实际大小与上述正常模式相同
box-sizing: border-box; 除外边距外，盒子本身占有的实际大小包括边框、内边距、内容大小。
```
关于外边距塌陷（margin collapsing）
几种表现形式，以下针对块级元素
* 上下外边距不等

当两个上下排列的盒子，bottom 和 top 分别具有 margin 时，会有外边距组合的情况出现，这种行为被称为外边距塌陷（margin collapsing），而浏览器经过计算，最终会取两个盒子中较大的值。倘若含有负值，例如上面盒子为20px，下面为-20px，最终的表现则为 0。

* 子元素的外边距在父元素中也有体现

通俗来讲，是子元素中设置了margin 而父元素中没有除 margin 外若没有其他有关影响盒子宽高的描述，将会导致父元素在表层体现上也会具有margin。而且这两个合并成了一个。例如如下代码，父元素也会产生 margin 效果。

```html
<div>
  <div class="box" />
</div>
```
这种情况的发生，往往在父元素和第一个子元素或者最后一个子元素之间

空元素的上下 margin 会合并

```html
<div style="margin-top: 20px; margin-bottom: 20px;"></div>
```
上述代码中，该空元素与上下间隔为 20px。

总结
以上，都在说一种现象。所谓的CSS布局，看似有很多漏洞和不足，其实，都是编码的周全考虑。这样的计算方式看似不合理，实际上，对浏览器而言，根据这些规则绘制UI是非常友好的。总之，不要把自己想当然的东西作为一种常识记在心中，总有些不同角度的合理解释，这才是代码。


链接：http://www.imooc.com/article/21371
