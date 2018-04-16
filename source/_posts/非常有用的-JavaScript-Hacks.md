---
title: 非常有用的 JavaScript Hacks
date: 2018-04-08 16:26:08
tags: javascript
---

1.使用 !! 将变量转换为布尔值

有时我们需要检查一个变量是否存在或者是否是有效值。为了实现这个功能，你可以对变量应用使用 !! 操作符：!!variable，这可以把任何类型的值转换为布尔值，并且只有当这个变量的值为 0 / NULL /  " " / NaN 的时候才会返回 FALSE，其他情况都返回 TRUE。为了方便理解，我们看看下面的例子：

```bash
function Account(cash) {
    this.cash = cash;
    this.hasMoney = !!cash;
}
var account = new Account(100.50);
console.log(account.cash); // 100.50
console.log(account.hasMoney); // true

var emptyAccount = new Account(0);
console.log(emptyAccount.cash); // 0
console.log(emptyAccount.hasMoney); // false
这个例子中，只要 account.cash 的值大于 0 ，account.hasMoney 就将为 TRUE。
```

2.使用 + 转换为数值

这个非常赞，并且很容易实现，但它只能作用于字符串数值，否则就会返回 NaN（不是数字）。我们来看下面的例子：
```bash
function toNumber(strNumber) {
    return +strNumber;
}
console.log(toNumber("1234")); // 1234
console.log(toNumber("ACB")); // NaN
并且此方法也可作用于 Date 函数，这是它将返回时间戳：

console.log(+new Date()) // 1461288164385
```
3.减少条件代码

如果你看到这样的代码：
```bash
if (conected) {
    login();
}
```
你可以通过使用 && 操作符组合两个变量来缩短它。比如前面这段代码可以缩短为：
```bash
conected && login();
```
你也可以用这种方法检测一个类中的属性或者方法是否存在。类似的代码：
```bash
user && user.login();
```
4.使用 || 设置默认值

现在 ES6 中支持默认值参数。在比较旧的浏览器中模拟这一特性，你可以使用 || 操作符，通过将默认值设置为第二个参数来实现。如果第一个参数返回 FALSE，第二个值将被作为默认值，例如：
```bash
function User(name, age) {
    this.name = name || "Oliver Queen";
    this.age = age || 27;
}
var user1 = new User();
console.log(user1.name); // Oliver Queen
console.log(user1.age); // 27

var user2 = new User("Barry Allen", 25);
console.log(user2.name); // Barry Allen
console.log(user2.age); // 25
```
5.在循环中缓存 array.length

当在循环中处理很大的数组时，这个小技巧虽然很简单，却会带来巨大的性能提升。通常情况下，基本上所有人都会这么循环数组：
```bash
for(var i = 0; i < array.length; i++) {
    console.log(array[i]);
}
如果这是一个小的数组那还好，但如果是大数组，每一次循环都会重复计算数组的长度，所有就会产生一部分延迟。为了避免这种情况，你应当把 array.length 缓存到一个变量中，而不是在循环中每次计算 
array.length ：

var length = array.length;
for(var i = 0; i < length; i++) {
    console.log(array[i]);
}
更简化一些的话，你可以这么写：

for(var i = 0, length = array.length; i < length; i++) {
    console.log(array[i]);
}
```
6.检测对象中的属性

当你需要检测属性是否存在时，这个技巧非常有用，它可以避免运行未定义的方法或者属性。如果你计划编写跨浏览器的代码，你可能也需要此技能。例如，假设你需要编写兼容 IE6 的代码，并且想使用 document.querySelector() 根据它们的 ID 来获取元素。然而，在这个浏览器中此方法并不存在，所以你可以使用 in 操作符来检测其存在性，例如：
```bash
if ('querySelector' in document) {
    document.querySelector("#id");
} else {
    document.getElementById("id");
}
```
这时，如果 document 对象中不存在 querySelector 方法的话，将使用 document.getElementById() 作为回调。

7.获取数组中最后的元素

当你设置了 begin 和 end 两个参数的时候，Array.prototype.slice(begin, end) 方法可以剪切数组。但当你不设置 end 参数时，该函数将自动把它设置为数组的最大值。我想很多人可能不知道该函数可以接受负的参数。如果你设置一个负值的话，该函数将得到数组后面的元素：
```bash
var array = [1,2,3,4,5,6];
console.log(array.slice(-1)); // [6]
console.log(array.slice(-2)); // [5,6]
console.log(array.slice(-3)); // [4,5,6]
```
8.数组截断

这个技巧可以锁定数组的长度，当你需要根据你设置的元素个数来删除一些元素时，这个方法非常有帮助。比如，当数组中有 10 个元素，而你只想获取其中前 5 个的话，你可以截断数组，通过设置 array.length = 5 使其更小。看下面的例子：
```bash
var array = [1,2,3,4,5,6];
console.log(array.length); // 6
array.length = 3;
console.log(array.length); // 3
console.log(array); // [1,2,3]
```
9.全部替换

String.replace() 函数允许使用字符串和正则来替换字符串，默认情况下，它只会替换第一个出现的。但你可以通过在正则最后加上 /g 来模拟 replaceAll() 函数：
```bash
var string = "john john";
console.log(string.replace(/hn/, "ana")); // "joana john"
console.log(string.replace(/hn/g, "ana")); // "joana joana"
```
10.合并数组

如果你需要合并两个数组的话，可以使用 Array.concat()：
```bash
var array1 = [1,2,3];
var array2 = [4,5,6];
console.log(array1.concat(array2)); // [1,2,3,4,5,6];
然而，这个函数并不适用于合并大的数组，因为它需要创建一个新的数组，而这会消耗很多内存。这时，你可以使用 Array.push.apply(arr1, arr2) 来代替创建新的数组，它可以把第二个数组合并到第一个中，从而较少内存消耗：

var array1 = [1,2,3];
var array2 = [4,5,6];
console.log(array1.push.apply(array1, array2)); // [1,2,3,4,5,6];
```
11.把节点列表(NodeList)转换为数组

如果你运行 document.querySelectorAll("p") 方法，它可能会返回一个 DOM 元素的数组 — 节点列表对象。但这个对象并不具有数组的全部方法，如 sort(),reduce(), map(), filter()。为了使用数组的那些方法，你需要把它转换为数组。只需使用 [].slice.call(elements) 即可实现：
```bash
var elements = document.querySelectorAll("p"); // NodeList
var arrayElements = [].slice.call(elements); // 现在 NodeList 是一个数组
var arrayElements = Array.from(elements); // 这是另一种转换 NodeList 到 Array  的方法
```
12.打乱数组元素的顺序

```bash
var list = [1,2,3];
console.log(list.sort(function() { Math.random() - 0.5 })); // [2,1,3]
```