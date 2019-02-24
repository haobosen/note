## for in 循环

````
//通过判断让for in 只循环非原型链上的对象
for(var i in val){
 if (val.hasOwnProperty(i)) {
     
 }
}
````

## scrollTop 各个浏览器兼容