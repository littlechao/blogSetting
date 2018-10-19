---
title: redux记录
date: 2018-10-10 10:14:14
tags: redux
---

创建redux，中间件使用方法

<!--more-->
# 创建redux

## 创建action -action.js
```bash
export const ADD_TO_CART = 'ADD_TO_CART';
export function addToCart(product, quantity, unitCost) {
  return {
    type: ADD_TO_CART,
    payload: { product, quantity, unitCost } //传递的参数
    error:'' //可自己创建
  }
}
```

##创建reducer reducer.js
```bash
import  { ADD_TO_CART }  from '../action.js';

const initialState = {
  cart: [
    {
      product: 'bread 700g',
      quantity: 2,
      unitCost: 90
    }
  ]
}
export default function(state=initialState, action) {
  switch (action.type) {
    case ADD_TO_CART: {
      return {
        ...state,
        cart: [...state.cart, action.payload],
        carts: [...state.cart, action.payload]
      }
    }
    default:
      return state;
  }
}
```

##创建store.js初始化redux -index.js
```bash
import { combineReducers } from 'redux';
import reducer from 'reducer.js';
const allReducers = {
  example: reducer,
}
const rootReducer = combineReducers(allReducers);

export default rootReducer;
```

#调用
```bash
import store from 'index.js';

store.getState();  //获取store

let unsubscribe = store.subscribe(() =>   //监听数据变化
  console.log(store.getState())
);

store.dispatch(addToCart('Coffee 500gm', 1, 250));  //调用方法
```
#在router中配置store
```bash
import { Provider } from 'react-redux';
import { Route,HashRouter,Redirect} from "react-router-dom";
  ...
  render(
    <Provider store={store}>
      <HashRouter>
        <React.Fragment>   //代替空的div
          <Route path="/" exact render={App.onRedirct}/>
          <Route exact path="/home" component={Home} />
          <Bottom />
        </React.Fragment>
      </HashRouter>
    </Provider>
  )
```
##在例子home中调用store 
```bash
import { connect } from "react-redux";

const mapStateToProps = state => state.shoppingCart;
const mapDispatchToProps = (dispatch) => ({
  addToCart : (params) => dispatch(addToCart(params))
})
export default connect(mapStateToProps,mapDispatchToProps)(Home);

-- 通过connect中间件连接后在主键中就可调用store的变量或者函数：

componentDidMount(){
  console.log(this.props)  
  // {
    addToCart:function(){},
    cart:[{
      product: 'bread 700g',
      quantity: 2,
      unitCost: 90
    }],
    title: "Home"
  }
}
this.props.addToCart({product: 'bread 100g',quantity: 3,unitCost: 100})

--  用装饰器@引入

const mapDispatchToProps = (dispatch) => ({
  addToCart : (params) => dispatch(addToCart(params))
})
@connect(
  state => state.cart,
  mapDispatchToProps
)

若一个主键下面有许多子组件需要引入connect，减少冗余代码：  --connect.js

import {connect} from 'react-redux'

const mapDispatchToProps = (dispatch) => ({
  addToCart : (params) => dispatch(addToCart(params))
})
export default connect(
 state=>state.cart,
 mapDispatchToProps
)

引入：
import connect from 'connect.js'
@connect
```