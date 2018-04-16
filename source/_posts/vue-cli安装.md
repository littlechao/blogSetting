---
layout: w
title: vue-cli安装
date: 2018-03-28 16:54:55
tags: vue-cli
categories: vue
---


<!--more-->

1、安装vue-cli

```bash
npm install vue-cli -g
```

2、安装模板

```bash
vue init webpack-simple my-project-name(简洁)

vue init webpack my-project-name(完整)
```
 

3、使用sass

```bash
<style lang="scss">
</style>
```

使用element-ui,需要引入loader，配置webpack.base

```bash
{
    test: /\.(eot|svg|ttf|woff|woff2)(\?\S*)?$/,
    loader: 'file-loader'
},
{
    test: /\.(png|jpe?g|gif|svg)(\?\S*)?$/,
    loader: 'file-loader',
    query: {
        name: '[name].[ext]?[hash]'
    }
}
　　
//在项目下，运行下列命令行
npm install --save-dev sass-loader
//因为sass-loader依赖于node-sass，所以还要安装node-sass
npm install --save-dev node-sass
```