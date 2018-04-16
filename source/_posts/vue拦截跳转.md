---
title: vue拦截跳转
date: 2018-04-02 15:47:07
tags: vue
---

在vue中实现拦截跳转

<!-- more -->

```bash
router.beforeEach((to, from, next) => {
  // console.log('to:' + to.path)
  if (to.path.startsWith('/login')) {
    window.sessionStorage.removeItem('access-user')
    next()
  } else {  //如果不是跳转的登录页面，就需要验证是否存在storage,不存在就需要重新去登陆
    let user = JSON.parse(window.sessionStorage.getItem('access-user'))
    if (!user) {
      next({path: '/login'})
    } else {
      next()
    }
  }
})
```

vue跳转以及获取query或者params参数
```bash
 this.$router.push({path:'/login',query:{a:'1',b:'2'}});   //跳转页面
 console.log(this.$route.query)   //{a:'1',b:'2'}
 ```