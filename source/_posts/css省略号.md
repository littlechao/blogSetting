---
title: css省略号
date: 2018-07-23 16:19:57
tags:
---

<!--more-->

# 1、单行

```bash
overflow:hidden;
text-overflow:ellipsis;
white-space:nowrap
```

# 2、多行

```bash
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 2;
-webkit-box-orient: vertical;
```
移动端浏览器绝大部分是WebKit内核的，所以该方法适用于移动端