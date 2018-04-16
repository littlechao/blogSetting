---
title: 数组中迭代方法-js
date: 2018-03-30 10:26:41
tags: javascript
---

javascript中数组的迭代方法

<!--more-->

# var arr = [1,2,3,4]

> 1.forEach（让数组每一项做一件事情）

```bash
arr.forEach(function(item,index){
    console.log(item);
});
// console.log(1)  console.log(2) console.log(3)  console.log(4)
```

> 2.map(让数组通过某种计算产生一个新数组)

```bash
var newArr = arr.map(function(item,index){
  return item*2;
});
// newArr [2,4,6,8] 
```

> 3.filter(筛选出数组中符合条件的项，组成新的数组)

```bash
var newArr = arr.filter(function(item,index){
    return item>3;
});
// [4]
```

> 4.reduce(让数组的前项和后项做某种计算，并累计最终值)

```bash
var result = arr.filter(function(prev,next){
    return prev+next;
});
// result => 15
```

> 5.every(检测数组中的每项是否符合条件)

```bash
var result = arr.every(function(item,index){
    return item>0;
});
// result => true;(全部满足才为true)
```

> 6.some(检测数组中是否有符合条件)

```bash
var result = arr.some(function(item,index){
    return item>1;
});
// result => true;(只要满足一个就为true)
```