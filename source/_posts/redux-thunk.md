---
title: redux-thunk
date: 2018-10-13 12:20:37
tags:react
---

react中间件redux-thunk

<!--more-->

> Thunk middleware for Redux.

## npm install redux-thunk

## 应用
```bash
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers/index';

// Note: this API requires redux@>=3.1.0
const store = createStore(
  rootReducer,
  applyMiddleware(thunk)
);

```

[Redux 入门教程（二）：中间件与异步操作](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_two_async_operations.html)