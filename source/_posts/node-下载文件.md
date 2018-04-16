---
layout: w
title: node 下载文件
date: 2018-04-10 10:44:23
tags: nodejs
---

通过nodejs中fs模块下载文件并保存在文件夹中

<!--more-->

```bash
var fs = require("fs");
var http = require("http");
var url = require("url");

var execlURL = 'http://58.252.60.156:9000/execl/uploadTemplate.xlsx';
var options = url.parse(execlURL);

var req=http.request(options,function(res){
    // res.setEncoding("utf-8");
    var data = [];
    var size = 0;
    res.on("data",function(chunk){
        data.push(chunk);
        size+= chunk.length;
        // console.log(chunk.toString())
        // fs.writeFileSync('output.txt', chunk.toString(), function (err) {
        //     if (err) {
        //         console.log(err);
        //     } else {
        //         console.log('ok.');
        //     }
        // });
    });
    res.on("end",function(err){
        var dataTwo = Buffer.concat(data, size);
        var fileName = './execl/outputExectemplate.xlsx';
        fs.writeFileSync(fileName,dataTwo);
    });
    console.log(res.statusCode);
});
req.on("error",function(err){
    console.log(err.message);
});
req.end();
```