## for in 循环

````
//通过判断让for in 只循环非原型链上的对象
for(var i in val){
 if (val.hasOwnProperty(i)) {
     
 }
}
````

## scrollTop 各个浏览器兼容

````
if (document.documentElement.scrollTop == 0) {
    document.body.scrollTop = '0px';
}else {
    document.documentElement.scrollTop = '0px';        
}

````

## 对new的理解

创建了一个对this的绑定，用于实例化一个类
原理是类的构造函数被调用，并且实例化了新的对象。

## 获取数组中的最大值和最小值

````
var a=[1,2,3,5];
alert(Math.max.apply(null, a));//最大值
alert(Math.min.apply(null, a));//最小值
````

## 删除数组中的元素，删除之后，每个值的坐标改变，再次删除无法删除

````
function filterModule(moduleName) {
    for (var i = 0; navConArray.length > i; i++) {
        if (typeof moduleName == 'string') {
            if (navConArray[i].routerName == moduleName) {
                navConArray.splice(i, 1);
            }
        } else {
            for (var j = 0; moduleName.length > j; j++) {
                if (navConArray[i].routerName == moduleName[j]) {
                    navConArray.splice(i, 1);
                    i--;
                    break;
                }
            }
        }

    }
}
````

## 禁用长按选择文字，禁用长按弹出菜单

````
// 如果是想禁用长按弹出菜单, 用js  
window.addEventListener('contextmenu', function(e){  
    e.preventDefault();  
}); 
````

## apply, call 

````
用另一个对象替换当前对象

fn.call(this, options);

fn替换this，这样可以改变this的指向
````

## 对于jquery中offset().top的理解

offset().top 是元素距离document顶部的距离

如果document中的子元素可以滚动，offset().top可以计算出元素距离浏览器顶部的距离

如果整个document滚动，需要用offset().top减去$(window).scrollTop算出该元素距离浏览器顶部的距离

## 判断图片是否加载完成，加载完成后执行回调

````
function imgLoadingJudge(callback) {
    var loadImg = new Array();
    var imgIndex = 0;
    var imgGather = document.getElementsByTagName('img');

    for (var j = 0; j < imgGather.length; j++) {
        var img = new Image();
        img.src = imgGather[j].getAttribute('src');
        
        img.onload = function () {
            if (imgIndex == imgGather.length) {
                callback();
            }
            imgIndex++;
        }

    }
}
````

## 图片上传
ie，edge在触发选择文件弹窗后，会截停代码运行，其他浏览器不会截停

## onchange, onpropertychange, oninput

onpropertychange为IE专属, html元素属性发生改变即可立即捕获。

其他浏览器要想获得onpropertychange一样的效果，需要用到oninput，但ie9 以下不支持oninput

## 加载巨大图 优化方法

把图片放入自定义属性中，加载完成后替换到src里
````
    var img = new Image();
    img.src = $('img').attr('data-src');
    img.onload = function () {
        $("img").attr({
            'src': img.src
        });

    }
````

##变量未定义解决方法

使用typeof判断变量是否为undefind，不为undefind才能执行需要调用此变量的代码，为undefind不能执行。 
## 打造自己的视频播放器

https://segmentfault.com/a/1190000006461476

https://segmentfault.com/a/1190000006477658

https://segmentfault.com/a/1190000006569543

https://segmentfault.com/a/1190000006604046

## 简单路由
```
function Router() {
    this.routes = {};
    this.curUrl = '';

    this.route = function (path, callback) {

        this.routes[path] = callback || function () { };
                                    };

    this.refresh = function () {
    
        this.curUrl = location.hash.slice(1) || '/';
        this.routes[this.curUrl]();
    };

    this.init = function () {
        var that = this;

        $(document).ready(function(){
            that.refresh();
        })
            $(window).on('hashchange', function(){
            that.refresh();
        })
    }

}

var R = new Router();
R.init();

R.route('/', function () {

});
R.route('/intro', function () {

});
R.route('/monster', function () {

});
R.route('/group', function () {

});
R.route('/project', function () {

});
R.route('/qa', function () {

});

```

## 闭包    

```
 function xunhuan(num){
    var a = num;

    return function (n) {
        for (var i = 0; i < n; i++) {
            console.log(a++);
        }
    }
}

var fun = xunhuan(1);

fun(10);

```

## 获取url中的参数

```
function GetQueryString(name)
{
     var reg = new RegExp("(^|&)"+ name +"=([^&]*)(&|$)");
     var r = window.location.search.substr(1).match(reg);
     if(r!=null)return  unescape(r[2]); return null;
}
```

## blur事件优于click事件执行解决

###解决1：
    将click事件换成mousedown
###解决2：
    延迟执行blur，延迟二三百毫秒

## scroll事件多次执行处理

可以用布尔值判断，true执行，scroll执行完毕后改为false

## cookie操作

```
function cookieFun() { }

cookieFun.prototype = {
	setCookie: function (name, value, Hours) {
		var exp = new Date();
		exp.setTime(exp.getTime() + Hours * 60 * 60 * 1000);
		document.cookie = name + "=" + value + ";expires=" + exp.toGMTString() + ";path=/;domain=sanjieke.cn";
	},
	getCookie: function (name) {
		var arr, reg = new RegExp("(^| )" + name + "=([^;]*)(;|$)");
		if (arr = document.cookie.match(reg))
			return unescape(arr[2]);
		else
			return null;
	}
}
```

## 解决多行文本溢出显示省略号

```
function wordlimit(cname, wordlength) {//1.首先，定义函数，其中两个参数，参数一是目标元素，也就是需要显示省略号的那个元素；参数二是需要限制的字数。

    var cname = document.getElementsByClassName(cname);//2.定义变量cname，即目标元素

    for (var i = 0; i < cname.length; i++) {//3.这里写了个循环，因为目标元素不止一个，之前找到一个通过获取id来截取字段实现效果的，但是如果目标元素有多个，id每个又不能相同，就显得麻烦了

        　　　　var nowLength = cname[i].innerText.length;//4.定义变量nowLength，里面存储的是每一个目标元素所包含的字数。
               
        　　　　if (nowLength > wordlength) {//这里做一些判断，如果现在的每个目标元素里面的字数多于我们需要限制的字数
            　　　　　　cname[i].innerText = cname[i].innerText.substr(0, wordlength) + ' . . .';//每个目标元素的内容就会被改变为当前内容的字符长度从0开始然后一直截取到需要限制的字数位置。

        　　　　}

    　　}

}

wordlimit("s_con", 52)
```

## 判断图片是否加载完成，可获取进度

imgLoad.js

```
(function () {
    function isArray(obj) {
        return Object.prototype.toString.call(obj) === '[object Array]';
    }

    /**
     * @param imgList 要加载的图片地址列表，['aa/asd.png','aa/xxx.png']
     * @param callback 每成功加载一个图片之后的回调，并传入“已加载的图片总数/要加载的图片总数”表示进度
     * @param timeout 每个图片加载的超时时间，默认为5s
     */
    var loader = function (imgList, callback, timeout) {
        timeout = timeout || 5000;
        imgList = isArray(imgList) && imgList || [];
        callback = typeof(callback) === 'function' && callback;

        var total = imgList.length,
            loaded = 0,
            imgages = [],
            _on = function () {
                loaded < total && (++loaded, callback && callback(loaded / total));
            };

        if (!total) {
            return callback && callback(1);
        }

        for (var i = 0; i < total; i++) {
            imgages[i] = new Image();
            imgages[i].onload = imgages[i].onerror = _on;
            imgages[i].src = imgList[i];
        }

        /**
         * 如果timeout * total时间范围内，仍有图片未加载出来（判断条件是loaded < total），通知外部环境所有图片均已加载
         * 目的是避免用户等待时间过长
         */
        setTimeout(function () {
            loaded < total && (loaded = total, callback && callback(loaded / total));
        }, timeout * total);

    };

    "function" === typeof define && define.cmd ? define(function () {
        return loader
    }) : window.imgLoader = loader;
})();

```

js中引用

```
imgLoader(['http://cdn.sanjieke.cn/condom/title.png', 'http://cdn.sanjieke.cn/condom/indexgif.gif'], function(percentage){
    console.log(percentage)
});
```

## ios下的微信打开的页面背景音乐无法自动播放

·本文的解决方案的核心是利用了 微信/易信 在ready的时候会有个 WeixinJSBridgeReady/YixinJSBridgeReady事件，通过监听这个事件来触发的。那有个坑就是 如果微信已经ready了，但还没执行到你监听这个ready事件的代码，那么你的监听是没用的，所以监听的js一定要放在head前面(放在css外链之前)，确保最新执行，切记！切记！。

·另一个坑就是，本文的解决方案只适合一开始就播放的背景音乐。如果你是做那种微信场景（打开页面模拟收到很多条微信，每条微信都要播放那段音效），实际上本文的解决方案是不行的。因为ready的事件只会执行一次，即使你在ready事件里面用setTimeout或者setInterval也可能会导致丢失情况。

在做各种HTML5场景页面的时候，插入背景音乐是一个很普遍的需求。我们都知道，IOS下的safari是无法自动播放音乐的，以至一直以来造成一种错误的认识，iso是无法自动播放媒体资源的。直到微信火爆起来，我们发现IOS的微信里面打开的页面却可以实现自动播放。这种情况颠覆了我之前的认知。但是，但是。。。最近的项目，又发现了一个头疼的问题。部分的IOS微信，打开有自动播放背景音乐的页面没有声音！！最头疼的是同款机子，相同的IOS系统，相同的微信版本！！没错，前端就是要经常这么折腾的，同一个问题，你以为找到了最终的解决方案，但是各种浏览器更新快速，昨天没问题，也许今天就有问题了。还好，这个问题暂时找到原因了，详情请看下文。

解决方案

先看下平时使用audio标签插入背景音乐的代码：

```
<audio id="Jaudio" class="media-audio" src="bg.mp3" autoplay preload loop="loop"></audio >
```
正常来说，上面的写法在安卓和大部分IOS机子的微信是可以播放的（safari这里就忽略讨论），可以扫一扫demo测试下你的手机或者点击查看demo>>：



如果上面的demo，你的ios微信可以播放，说明你的是大部分正常的手机。如果不能播放，哈哈，你成为了少部分不能正常播放的幸运者。。。

那代码有办法解决这少部分用户呢？如何解决呢？

答案的关键就是微信的WeixinJSBridgeReady事件。这个是微信自带提供的事件，测试发现，上面说的少部分的机子微信只要做微信ready后执行播放，就可以用代码实现自动播放功能了！具体代码请看下面：

```
<audio id="Jaudio" class="media-audio" src="bg.mp3" preload loop="loop"></audio >
function audioAutoPlay(id){
    var audio = document.getElementById(id);
    audio.play();
    document.addEventListener("WeixinJSBridgeReady", function () {
            audio.play();
    }, false);
}
audioAutoPlay('Jaudio');
```
刚才如果你第一个demo不能播放的童鞋可以再扫一扫测试下或者点击查看demo>>（如果第一个demo已经测试正常的，这个肯定是正常的啦）



是不是听到声音了呢？！！解决方案就是这么简单。

后语

总结下吧，关于音乐自动播放的问题，现在可以分为三种：

1-支持audio的autoplay，大部分安卓机子的自带浏览器和微信，大部分的IOS微信（无需特殊解决）

2-不支持audio的autoplay，部分的IOS微信（本文提供的解决方案）

3-不支持audio的autoplay，部分的安卓机子的自带浏览器（比如小米，开始模仿safari）和全部的ios safari（这种只能做用户触屏时就触发播放了）

那么针对已知的三种情况，关于自动播放背景音乐的问题，我们来总结一下综合解决方案代码吧：

```
<!DOCTYPE HTML>
<html>
<head>
<meta charset="utf-8">
<meta name="format-detection" content="telephone=no"/>
<title>IOS微信</title>
<meta name="keywords" content="" />
<meta name="description" content="" />
<script type="text/javascript">
//原来是在微信易信执行Ready之前，先注册事件，所以放在所有请求的最前面
document.addEventListener("WeixinJSBridgeReady", function () {
    audioAutoPlay('Jaudio');//给个全局函数
}, false);
document.addEventListener('YixinJSBridgeReady', function() {
    audioAutoPlay('Jaudio');//给个全局函数
}, false);
</script>
<!-- 加载css放这里 -->
</head>
<body>
  
<audio id="Jaudio" class="media-audio" src="http://game.163.com/weixin/gfxm3_gc/images/bg.mp3" preload loop="loop">
</audio>
  
<script>
function audioAutoPlay(id){//全局控制播放函数
    var audio = document.getElementById(id),
        play = function(){
            audio.play();
            document.removeEventListener("touchstart",play, false);
        };
    audio.play();
    document.addEventListener("touchstart",play, false);
}
 
var isAppInside=/micromessenger/i.test(navigator.userAgent.toLowerCase())||/yixin/i.test(navigator.userAgent.toLowerCase());
if(!isAppInside){//给非微信易信浏览器
  audioAutoPlay();
}
</script>
</body>
</html>
```

## forEach

[]只能是nodelist节点集合
forEach只能遍历节点集合
[].forEach(val, index, array){}

## ajax跨域解决  

在ajax中加入参数header

```
headers:{"X-Requested-With":"XMLHttpRequest"}
```

## js动态加载js

jquery

```
$.getScript("../jquery.js"); //加载jquery
$.getScript("../jquery.js",function(){  //加载完jquery之后执行function
    console.log('加载完成')
})
```

```
function loadScript(url, callback) {
  var script = document.createElement("script");
  script.type = "text/javascript";
  if(typeof(callback) != "undefined"){
    if (script.readyState) {
      script.onreadystatechange = function () {
        if (script.readyState == "loaded" || script.readyState == "complete") {
          script.onreadystatechange = null;
          callback();
        }
      };
    } else {
      script.onload = function () {
        callback();
      };
    }
  }
  script.src = url;
  document.body.appendChild(script);
}
loadScript("jquery-latest.js", function () { //加载,并执行回调函数
  alert($(window).height());
});
//loadScript("jquery-latest.js"); //加载js文件
```

## 利用jquery禁止外层滚动条的滚动

```
var scrollTop = -1; // 鼠标进入到区域后，则存储当前window滚动条的高度
        $('.pa-con').hover(function(){
            scrollTop = $(window).scrollTop();
        }, function(){
            scrollTop = -1;
        });

        // 鼠标进入到区域后，则强制window滚动条的高度
        $(window).scroll(function(){
            scrollTop!==-1 && $(this).scrollTop(scrollTop);
        })

```

## 从父页面获取iframe中的内容

```
$("iframe").contents();
```

## 判断字节大小

```
function zf(Words){
    var W = new Object();
    var iNumwords = 0;
    var sNumwords = 0;
    var sTotal = 0;
    var iTotal = 0;
    var eTotal = 0;
    var inum = 0;
    for (i = 0; i < Words.length; i++) {
      var c = Words.charAt(i);
      
      
      if (c.match(/[\u4e00-\u9fa5]/)) {
        if (isNaN(W[c])) {
          iNumwords++;
          W[c] = 1;
        }
        iTotal++;
      }
    }
    for (i = 0; i < Words.length; i++) {
      var c = Words.charAt(i);
      //双字节字符 汉字，汉字标点
      if (c.match(/[^\x00-\xff]/)) {
        if (isNaN(W[c])) {
          sNumwords++;
        }
        sTotal++;
      } else {
        eTotal++;
      }
      if (c.match(/[0-9]/)) {
        inum++;
      }
    }
    var zf =  iTotal * 2 + (sTotal - iTotal) * 2 + eTotal;
    return zf;
  }
```

## js confirm方法

点击取消返回false；确认返回true；

```
if(confirm('确认')){
    return true;
}else{
    return false;
}

```

## animate兼容谷歌火狐

```
$('body').animate();//只被谷歌兼容
$('html').animate();//只被火狐兼容
$('html,body').animate();//谷歌火狐同时兼容

```

## 关闭刷新页面弹窗

```
  //关闭,刷新页面提示
    $(window).bind("beforeunload",function(){
        return "建议点击底部“提交”按钮后离开，否则内容将丢失！";
    });

```

## 禁用移动端浏览器窗口上下滑动
   
``` 
    $("body").on("touchmove", function (event) {event.preventDefault();});

    document.addEventListener("touchmove", function(e){console.log(e.touches.length);e.preventDefault()}, false);

```

## json数据处理

```
JSON.parse(  ); 将json字符串转换为对象
JSON.stringify(  ); 将数组转换为JSON字符串

```

## iframe调用外部函数

```
$( ‘ window.parent.function() ‘ );

```

## 判断各浏览器，各种手机平台

```
function browser() {
    var u = navigator.userAgent.toLowerCase();
    var app = navigator.appVersion.toLowerCase();
    return {
        txt: u, // 浏览器版本信息
        version: (u.match(/.+(?:rv|it|ra|ie)[\/: ]([\d.]+)/) || [])[1], // 版本号
        msie: /msie/.test(u) && !/opera/.test(u), // IE内核
        mozilla: /mozilla/.test(u) && !/(compatible|webkit)/.test(u), // 火狐浏览器
        safari: /safari/.test(u) && !/chrome/.test(u), //是否为safair
        chrome: /chrome/.test(u), //是否为chrome
        opera: /opera/.test(u), //是否为oprea
        presto: u.indexOf('presto/') > -1, //opera内核
        webKit: u.indexOf('applewebkit/') > -1, //苹果、谷歌内核
        gecko: u.indexOf('gecko/') > -1 && u.indexOf('khtml') == -1, //火狐内核
        mobile: !!u.match(/applewebkit.*mobile.*/), //是否为移动终端
        ios: !!u.match(/\(i[^;]+;( u;)? cpu.+mac os x/), //ios终端
        android: u.indexOf('android') > -1, //android终端
        iPhone: u.indexOf('iphone') > -1, //是否为iPhone
        iPad: u.indexOf('ipad') > -1, //是否iPad
        webApp: !!u.match(/applewebkit.*mobile.*/) && u.indexOf('safari/') == -1 //是否web应该程序，没有头部与底部
    };
}
```
```
function getBrowserInfo() {
    var Sys = {};
    var ua = navigator.userAgent.toLowerCase();
    var re = /(msie|firefox|chrome|opera|version).*?([\d.]+)/;
    var m = ua.match(re);
    Sys.browser = m[1].replace(/version/, "'safari");
    Sys.ver = m[2];
    Sys.isIE11 = /trident.*rv:11/i.test(ua);
    return Sys;
}

var browser = getBrowserInfo();
var bver = parseInt(browser.ver);
if (browser.browser == 'chrome') {
    
} else if (browser.browser == 'firefox') {
    
} else if (browser.browser == "'safari") {

} else if (browser.isIE11) {
    
} else {
    
}
```

## 是否是微信端

```
function is_weixn(){  
    var ua = navigator.userAgent.toLowerCase();  
    if(ua.match(/MicroMessenger/i)=="micromessenger") {  
        return true;  
    } else {  
        return false;  
    }  
}  
```

## ie版本判断

```
if(navigator.appName == "Microsoft Internet Explorer" && navigator.appVersion .split(";")[1].replace(/[ ]/g,"")=="MSIE6.0" || navigator.appName == "Microsoft Internet Explorer" && navigator.appVersion .split(";")[1].replace(/[ ]/g,"")=="MSIE7.0" || navigator.appName == "Microsoft Internet Explorer" && navigator.appVersion .split(";")[1].replace(/[ ]/g,"")=="MSIE8.0" || navigator.appName == "Microsoft Internet Explorer" && navigator.appVersion .split(";")[1].replace(/[ ]/g,"")=="MSIE9.0")
{
alert("您的浏览器版本过低，请下载IE9以上版本");
}
```

## 大量图片按顺序加载
 
```
var imageAssets = ["https://drscdn.500px.org/photo/169459349/q%3D80_m%3D2000/9ea2638c46e1fd94570a5c9cd745c071","https://drscdn.500px.org/photo/169443083/q%3D80_m%3D2000/366605f8ccb33ab8402b15d707a41e76","https://drscdn.500px.org/photo/169454291/q%3D80_m%3D2000/c1cc0c422377ac717e02277982e0298e","https://drscdn.500px.org/photo/169444659/q%3D80_m%3D2000/694c15a70460478dbfe395ac3b2fddf7","https://drscdn.500px.org/photo/169429241/q%3D80_m%3D2000/c5e969c7a708d5ed15b74f2550b290a2","https://drscdn.500px.org/photo/169470895/q%3D80_m%3D2000/0f70733d38d917fc8e43c951f2835370"];

// 预加载
//        for (var i = 0; i < imageAssets.length; i++) {
//            new Image().src = imageAssets[i];
//        }

// 按数组数据加载
        var i = 0,timer = null,len = imageAssets.length;
        var load = function(src){
            if(i <= len){
                var img_obj = new Image;
                img_obj.src = src;
                timer = setInterval(function(){
                    if(img_obj.complete){
                        clearInterval(timer);
                        load(imageAssets[i++]);
                    }
                },80);
            }else{
                console.log("成功");
            }
        };
        load(imageAssets[i]);

```

## input file  文件api
### 文件对象：

```
var file = document.getElementById( “id” ).files[ 0 ]
```

### 判断上传文件是否是图片

```
if ( !( /\.( gif | jpg | jpeg | png | GIF | JPG | PNG )$/.test( file.name ) ) )
```

### 上传的图片并显示

```
if ( file ) {
     var reader = new FIleReader(  ) ;
     reader.onload = function () {
          // 将图片输出到img标签中
          $( “ <img src=‘“+ this.result +”'/> “ ).appendTo(“body");
     }
     reader.readAsDataURL( file );
}
```

#














