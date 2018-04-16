---
title: 闭包-javascript
date: 2018-04-02 09:54:31
tags: js闭包
---

有一个li列表，点击点击对应的列表弹出相应的序号

<!--more-->

html如下：
```bash 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body onload="onMyLoad()">
    <p>一</p>
    <p>二</p>
    <p>三</p>
    <p>四</p>
    <p>五</p>
</body>
</html>
```

  一般看到这种需求可能会直接写出代码：
```bash
    function onMyLoad(){
        var arr = document.getElementsByTagName("p");
        for(var i = 0; i < arr.length;i++){
            arr[i].onclick = function(){
                alert(i);
            }
        }
    }
    但是这样写并不会点一次弹出相应的序号，而是全部是alert(4);
```

# 若要实现就需换种方法
方法一：
```bash
for(var i = 0;i<arr.length;i++){
    //声明一个匿名函数,若传进来的是基本类型则为值传递,故不会对实参产生影响,
    //该函数对象有一个本地私有变量arg(形参) ,该函数的 function scope 的 closure 对象属性有两个引用,一个是 arr,一个是 i
    尽管引用 i 的值随外部改变 ,但本地私有变量(形参) arg 不会受影响,其值在一开始被调用的时候就决定了.
    (function (arg) {
        arr[i].onclick = function () {  //onclick函数实例的 function scope 的 closure 对象属性有一个引用 arg,
            alert(arg);                 //只要 外部空间的 arg 不变,这里的引用值当然不会改变
        }
    })(i);                              //立刻执行该匿名函数,传递下标 i(实参)
}
```

方法二：
```bash 
for(var i = 0;i<arr.length;i++){
    //为当前数组项即当前 p 对象添加一个名为 i 的属性,值为循环体的 i 变量的值,
    //此时当前 p 对象的 i 属性并不是对循环体的 i 变量的引用,而是一个独立p 对象的属性,属性值在声明的时候就确定了
    //(基本类型的值都是存在栈中的,当有一个基本类型变量声明其等于另一个基本变量时,此时并不是两个基本类型变量都指向一个值,而是各自有各自的值,但值是相等的)
    arr[i].i = i;
    arr[i].onclick = function () {
        alert(this.i);
    }
}
```

方法三：
```bash 
for(var i = 0; i<arr.length;i++){
    arr[i].onclick = (function(arg){
        return function () {
            alert(arg);
        }
    })(i);
}
```

方法四：
```bash 
for(var i = 0; i<arr.length;i++){
    (function(){
        var temp = i;
        arr[i].onclick = function () {
            alert(temp);
        }
    })();
}
```
 
方法五：
```bash 
for(var i = 0;i<arr.length;i++){
    arr[i].onclick = (function () {
        var temp = i;
        return function () {
            alert(temp);
        }
    })();
}
```

方法六：
```bash 
for(var i = 0;i<arr.length;i++){
    (arr[i].onclick = function () {
        alert(arguments.callee.i);      //arguments 参数对象  arguments.callee 参数对象所属函数
    }).i = i;
}
```   