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





