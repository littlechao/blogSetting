---
title: vue-router传参数（get和post方式）
date: 2018-04-20 11:39:31
tags:
---


# 1、get方式
```bash
页面跳转
 this.$router.push({path:'/xxx',query:{id:1}});//类似get传参，通过URL传递参数

新页面接收参数
 this.$route.query.id
```

# 2、post方式
```bash
页面跳转
  //由于动态路由也是传递params的，所以在 this.$router.push() 方法中 path不能和params一起使用，否则params将无效。
需要用name来指定页面。
 this.$router.push({name:'page2',params:{id:1}});//类似post传参

新页面接收参数
 this.$route.params.id
 ````