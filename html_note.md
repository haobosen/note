## 两个span之间的间距怎么解决掉

```
div{
    width:100%;
    font-size:0;
}

span{
    padding:1% 2%;
    font-size:16px;
    background:#ddd;
}

这样就可以了。应该是你把span设置为块级元素了，然后div有字体大小，span外边有空格所以会有空隙，改字体为0然后再单独设置span里面的字体大小就解决了。 
```

## DOM更新，之前绑定的事件丢失

原生js，使用innerHTML，会将其父元素中的所有子元素dom全部更新一遍，这样会导致之前绑定的事件全部失效。

解决：
通过给父元素绑定事件，利用事件冒泡，在点击dom时，判断是否是需要触发事件的dom，如果是，就去执行相应的回调，不是就不执行

jquery的on绑定事件，就是先给document绑定事件，然后利用冒泡，去判断点击的元素是否是需要触发的dom来执行回调

## html meta 标签总结介绍

https://segmentfault.com/a/1190000004279791

### <!DOCTYPE>

所有浏览器都支持<!DOCTYPE>
### 概念

 是指web浏览器关于页面使用哪个html版本进行编写的指令。


### 常用DOCTYPE声明

#### html 5

```
<!DOCTYPE html>
```

#### html 4.01(共三种)
##### 1. html 4.01 Strict

该 DTD 包含所有 HTML 元素和属性，但不包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```
##### 2. html 4.01 Transitional

该 DTD 包含所有 HTML 元素和属性，包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
"http://www.w3.org/TR/html4/loose.dtd">
```
##### 3. html 4.01 Frameset

该 DTD 等同于 HTML 4.01 Transitional，但允许框架集内容。

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" 
"http://www.w3.org/TR/html4/frameset.dtd">
```

#### XHTML 1.0(共三种)
##### 1. XHTML 1.0 Strict

该 DTD 包含所有 HTML 元素和属性，但不包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。必须以格式正确的 XML 来编写标记。

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" 
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```
##### 2. XHTML 1.0 Transitional

该 DTD 包含所有 HTML 元素和属性，包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。必须以格式正确的 XML 来编写标记。

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "
http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```
##### 3. XHTML 1.0 Frameset

该 DTD 等同于 XHTML 1.0 Transitional，但允许框架集内容。

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" 
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
```

#### XHTML 1.1

该 DTD 等同于 XHTML 1.0 Strict，但允许添加模型（例如提供对东亚语系的 ruby 支持）。

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
```

## a标签在火狐浏览器中会跳空页面

```
<a href="javascript:void(0)"></a>
```

## 清除H5文件缓存

chrome访问
chrome://appcache-internals/

## input元素默认会有间距

input是内联元素inline-block, 内联元素处理会当成文字处理，文字间会有间距，将input的父元素字号设置为0可解决


## HTML中的6种空格
HTML提供了5种空格实体（space entity），它们拥有不同的宽度，非断行空格（& nbsp;）是常规空格的宽度，可运行于所有主流浏览器。其他几种空格（ & ensp; & emsp; & thinsp; & zwnj;& zwj;）在不同浏览器中宽度各异。

### & nbsp;

它叫不换行空格，全称No-Break Space，它是最常见和我们使用最多的空格，大多数的人可能只接触了& nbsp;，它是按下space键产生的空格。在HTML中，如果你用空格键产生此空格，空格是不会累加的（只算1个）。要使用html实体表示才可累加，该空格占据宽度受字体影响明显而强烈。

### & ensp;

它叫“半角空格”，全称是En Space，en是字体排印学的计量单位，为em宽度的一半。根据定义，它等同于字体度的一半（如16px字体中就是8px）。名义上是小写字母n的宽度。此空格传承空格家族一贯的特性：透明的，此空格有个相当稳健的特性，就是其占据的宽度正好是1/2个中文宽度，而且基本上不受字体影响。

### & emsp;

它叫“全角空格”，全称是Em Space，em是字体排印学的计量单位，相当于当前指定的点数。例如，1 em在16px的字体中就是16px。此空格也传承空格家族一贯的特性：透明的，此空格也有个相当稳健的特性，就是其占据的宽度正好是1个中文宽度，而且基本上不受字体影响。

### & thinsp;

它叫窄空格，全称是Thin Space。我们不妨称之为“瘦弱空格”，就是该空格长得比较瘦弱，身体单薄，占据的宽度比较小。它是em之六分之一宽。

### & zwnj;

它叫零宽不连字，全称是Zero Width Non Joiner，简称“ZWNJ”，是一个不打印字符，放在电子文本的两个字符之间，抑制本来会发生的连字，而是以这两个字符原本的字形来绘制。Unicode中的零宽不连字字符映射为“”（zero width non-joiner，U+200C），HTML字符值引用为： & #8204;

### & zwj;

它叫零宽连字，全称是Zero Width Joiner，简称“ZWJ”，是一个不打印字符，放在某些需要复杂排版语言（如阿拉伯语、印地语）的两个字符之间，使得这两个本不会发生连字的字符产生了连字效果。零宽连字符的Unicode码位是U+200D (HTML: & #8205; & zwj;）。

此外，浏览器还会把以下字符当作空白进行解析：空格（& #x0020;）、制表位（& #x0009;）、换行（& #x000A;）和回车（& #x000D;）还有（& #12288;）等等。

