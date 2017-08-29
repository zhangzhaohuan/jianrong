# jianrong
## 获取滚动距离的兼容
```
//非chrome
document.documentElement.scrollTop   
document.documentElement.scrollLeft

//chrome
document.body.scrollTop
document.body.scrollLeft

//兼容写法：由于浏览器只支持其中一种，另一种为0，因此采用相加的方式
var scrolltop = document.documentElement.scrollTop + document.body.scrollTop

//更为稳妥的兼容写法：
var scrolltop = document.documentElement.scrollTop || document.body.scrollTop

```
## getElementsByClassName()
```
if(!document.getElementsByClassName){ //如果不存在该方法
    document.getElementsByClassName = function(classname){ //则手动创建
          var arr = []; 
          var all = document.getElementsByTagName("*");
          for(var i=0; i<all.length; i++){
               if(all[i].className.indexOf(classname+" ") != -1){
                    arr.push(all[i]); 
               }
          }
          return arr;
    } 
}

```
## JS获取非行内样式
```
window.getComputedStyle(ele, null)      //非IE(IE6,7,8)
ele.currentStyle      //IE(ie6,7,8)

function getStyle(obj, attr) {
    if(obj.currentStyle) { //IE浏览器
        return obj.currentStyle[attr];
    } else {
        return getComputedStyle(obj,null)[attr];
    }
}     

```
## 获取Event对象的兼容写法
```
obj.xxxx = function(evt){
     var e = evt || window.event;
}

```

## 键盘码获取
```
e.keyCode || e.which
```
## 阻止事件传播
```
e.stopPropagation ? e.stopPropagation() : e.cancelBubble = true;
```
## 事件对象目标
```
var srcObj = event.target || event.srcElement;
```
## 阻止默认行为
```
event.preventDefault();
event.returnValue = false;
e.preventDefault ? e.preventDefault() : e.returnValue=false;

```
## 事件监听
```
obj.addEventListener("click",function(){},true);   //非IE

obj.attachEvent("onclick", function(){});      //IE

function addEvent(ele, eventType, func, isCapture){
     if(ele && ele.attachEvent){
          ele.attachEvent("on"+eventType, func);
     } else {
          ele.addEventListener(eventType, func, isCapture||false);
     }
}


```

## request对象的兼容
```
new ActiveXObject("Msxml2.XMLHTTP")   //IE

var req = ActiveXObject?new ActiveXObject("Msxml2.XMLHTTP"):new XMLHttpRequest() ;

```
