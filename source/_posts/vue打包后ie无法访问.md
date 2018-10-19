---
title: vue打包后ie无法访问
date: 2018-09-25 16:38:43
tags:
---
---

vue打包后ie无法访问


> 1.安装 babel-polyfill 
> 2.在入口文件中引用：import 'babel-polyfill'

<!-- more -->

# 1,2步无法生效，修改webpack.base.conf.js中配置
```bash
entry: {
app: ["babel-polyfill","./src/main.js"],
}

entry: {
app: "./src/main.js",
"babel-polyfill":"babel-polyfill"
}
```