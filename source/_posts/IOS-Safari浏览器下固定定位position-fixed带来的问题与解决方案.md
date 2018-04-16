---
title: 'IOS Safari浏览器下固定定位position:fixed带来的问题与解决方案'
date: 2018-04-04 14:55:01
tags: css
---

当我们在开发移动端页面时使用固定定位position:fixed时会发现，在IOS下运行会出现几个问题： 
1.页面滑动失去惯性，滑动不流畅。 
2.使用fixed定位的元素会随着页面的滑动而抖动，其中固定在底部的input唤起输入法会顶出一段距离。

<!--more-->

* -webkit-overflow-scroll:touch解决滑动无惯性  

## 解决第二个问题：
1.通过布局解决

```bash
css部分：
//我是吸顶头部
.header{
    width:100%;
    height:50px;
    position:fixed;
    top:0px;
}
//我是中间要滑动的部分
.main{
    width:100%;
    height:auto;
    position:absolute;
    padding-top:50px;/*top值为header的高*/
    padding-bottom:50px;/*bottom值为footer的高*/
    box-sizing:border-box;/*这里改变盒子模型为怪异盒模型，这样padding值不会增加main的高度*/
    overflow-y:scroll;
}
//我是吸底尾部
.footer{
    width:100%;
    height:50px;
    position:fixed;
    bottom:0px;
}
html部分：
<div class="header">
    <!--写点啥吧-->
</div>

<div class="main">
    <!--写点啥吧-->
</div>

<div class="footer">
    <!--写点啥吧-->
</div>

```
2.布局结合js动态实现
```bash
html部分：
<div class="content">
    ...内容
</div>
<div class="footer">
    <!--fixed布局的底部-->
</div>
//因为fixed在安卓上面能正常使用，所以只有当浏览器为ios才使用：
var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Adr') > -1; //android终端
var isiOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端
$('.content').css({'height':$(window).height()-$('.footer').height()});
if(isiOS){
    $('.footer').css({"position":"relative"});
}
if(isAndroid){
    $('.footer').css({"position":"fixed","bottom":"0"});
}
```