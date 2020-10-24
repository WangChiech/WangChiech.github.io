---
layout: post
title: "前端面试题vue、webpack"
subtitle: ''
author: "WangChiech"
header-style: text
tags:
  - 工程化

---

## browsersync

浏览器同步测试工具

> 1. 浏览器自动刷新
> 2. 多终端同步

使用步骤

1. 安装 
   	npm install -g browser-sync

2. 命令行要进入到对应的文件夹

3. 启动

   - `browser-sync start --server --files "*"`

     "*" 代表监听所有的文件 

   - `browser-sync start --server --files "css/*.css"`
     监听所有css文件

   - `browser-sync start --server --files "css/*.css, *.html"`
     监听所有css与html文件，多种文件中间以逗号隔开

> 底层实现原理为websocket