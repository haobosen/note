## iphone手机使用on绑定click事件无效

在on绑定的层样式里加入cursor：pointer

## 解决:hover、before、after伪类在ios移动端需要二次点击的问题

在body上绑定一个空的touchstart事件即可。

````
document.body.addEventListener('touchend', function(){ }); //touchstart  解决:hover伪类在移动端二次点击的问题
````

## css a元素相对于父元素fixed

父元素relative

子元素absolute

子元素中的a元素fixed

## ios移动端，js时间操作getTime(),getFullYear()等返回显示NaN的解决办法及原因

iOS上缺不能正常显示，显示的时间为：NaN-NaN1-NaN

解决办法

new Date("2018-02-15 20:30:00".replace(/-/g,'/')).getTime(); 

## 实现左右固定，中间自适应布局方法

圣杯

双飞翼

flex

绝对定位

https://blog.csdn.net/wangchengiii/article/details/77926868

## 选择所有子元素中的同一类名的元素

first-of-type

last-of-type 

## 单行多行文字水平垂直居中

````
父元素设置 
display: inline-block;
line-height: 父元素高度;
text-align: center;

子元素设置 
display: inline-block;
vertical-align: middle;
line-height: 26px;
                        
````

## 用div实现textarea的placeholder功能

```
<!DOCTYPE <html>  
<head>  
<title></title>  
<style type="text/css">  
.input{  
width:200px;  
height:30px;  
border:1px solid grey;  
}  
.input:empty::before{  
color:lightgrey;  
content:attr(placeholder);  
}  
</style>  
</head>  
<body>  
<div class="input" contenteditable placeholder="请输入文字"></div>  
</body>  
</html>
```

## ios 点击input 不获取焦点

```
* {  
    -webkit-touch-callout:none;  
    -webkit-user-select:none;  
    -khtml-user-select:none;  
    -moz-user-select:none;  
    -ms-user-select:none;  
    user-select:none;  
} 
```

## input type="number",去掉上下小箭头

### 在chrome下：

```
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button{
    -webkit-appearance: none !important;
    margin: 0; 
}
```
### Firefox下：

```
input[type="number"]{-moz-appearance:textfield;}
```

## 块级居中

```
html:
<div id="parent">
  <div id="child">Content here</div>
</div>
	
css:
#parent {display: table}

#child {
  display: table-cell;
  vertical-align: middle;
 }
 
IE Fix:
child {display: inline-block}
```

## margin-top 父div下落

解决方法： 
1、修改父元素的高度，增加padding-top样式模拟（padding-top：1px；常用） 
2、为父元素添加overflow：hidden；样式即可（完美） 
3、为父元素或者子元素声明浮动（float：left；可用） 
4、为父元素添加border（border:1px solid transparent可用） 
5、为父元素或者子元素声明绝对定位

## 修改placeholder颜色

```
textarea::-webkit-input-placeholder {
   /* WebKit browsers */
   color: #b5bec7;
}

textarea::-moz-placeholder {
    /* Mozilla Firefox 4 to 18 */
    color: #b5bec7;
}

textarea::-moz-placeholder {
    /* Mozilla Firefox 19+ */
    color: #b5bec7;
}

textarea::-ms-input-placeholder {
    /* Internet Explorer 10+ */
    color: #b5bec7;
}
```

### 修改placeholder颜色字体后，在ios显示，placeholder字体会显示不全

解决：

```
textarea::-webkit-input-placeholder {
   /* WebKit browsers */
   color: #b5bec7;
   font-size: 15px;
}
textarea {
    font-size: 16px; //该处的font-size值要大于placeholder里设置的字体大小
}
```

##解决ios中设置overflow：auto滚动不平滑

设置 -webkit-overflow-scrolling: touch;

## 移动端点击a链接出现蓝色色块解决方法

-webkit-tap-highlight-color是什么？

注释：

-webkit-tap-highlight-color 是一个 不规范的属性（unsupported WebKit property），它没有出现在 CSS 规范草案中。

当用户点击iOS的Safari浏览器中的链接或JavaScript的可点击的元素时，覆盖显示的高亮颜色。该属性可以只设置透明度。如果未设置透明度，iOS Safari使用默认的透明度。当透明度设为0，则会禁用此属性；当透明度设为1，元素在点击时不可见。

语法：

```
-webkit-tap-highlight-color：rgba(0,0,0,0)
```
默认值： inherit

适用于：链接元素比如新窗口打开，img元素比如保存图像等等

兼容性：

iOS 1.1.1及更高版本的Safari浏览器可用。大部分android手机也是支持的，只是显示效果有所不同。

##用省略号省略内容

在第二行用省略号

```
overflow: hidden;
display: -webkit-box;
-webkit-line-clamp: 2;
-webkit-box-orient: vertical;
word-break: break-all;
```

在第一行用省略号

```
overflow: hidden;
text-overflow:ellipsis;
white-space:nowrap;
```

## 去掉input button在点击时出现的蓝色边框

```
a,button,input{ 

-webkit-tap-highlight-color: rgba(0, 0, 0, 0);    

   -webkit-user-modify: read-write-plaintext-only;

}
```

可根据实际情况添加

```
outline: none;
```

或

```
box-shadow: none;
```

有时候<img/>图片放在a标签里也会出现边框，可设置图片的边框为0.

除此之外还要注意其伪类的设置。

js方法：

```
onclick="this.blur()"
```

## iPhone CSS media query（媒体查询）

### iPhone < 5:

```
@media screen and (device-aspect-ratio: 2/3) {}

```
### iPhone 5:

```
@media screen and (device-aspect-ratio: 40/71) {}
```

### iPhone 6:

```
@media screen and (device-aspect-ratio: 667/375) {}
```

### iPhone 6Plus:

```
@media screen and (device-aspect-ratio: 16/9) {}
```

### iPad:

```@media screen and (device-aspect-ratio: 3/4) {}
```

## css3 三角形

```
<style type="text/css">
.square{
    width: 200px;
    height: 80px;
    background: red;
}
.square:before {
    border-top: 100px solid #FFF;
    border-left: 30px solid transparent;
    border-right: 20px solid transparent;
    position: absolute;
    height: 0;
    width: 0;
    top: 0;
    left: 180px;
    display: block;
    content: '';
}
</style>
```

## css3 判断手机横竖屏

```
@media screen and (orientation:portrait) {
      // 竖屏
}

@media screen and (orientation:landscape) {
      // 横屏
}
```

```
@media all and (orientation : landscape) { /*这是匹配横屏的状态，横屏时的css代码*/
    body { 
        background-color: #ff0000; 
    } 
} 
@media all and (orientation : portrait){ /*这是匹配竖屏的状态，竖屏时的css代码　　*/
    body { 
        background-color: #00ff00; 
    } 
} 

```

