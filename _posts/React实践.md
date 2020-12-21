---
layout: post
title: "React实践"
subtitle: ''
author: "WangChiech"
header-style: text
tags:
  - 前端框架
---



[styled-components](https://styled-components.com/docs)

[react-transition-group](https://reactcommunity.org/react-transition-group/)

`standard.js` 规范

```js
1. npm install standard --save-dev
2. npm install snazzy --save-dev
3. 配置 package.json，添加一条名为 lint 的 npm script 
   "script": {"lint": "standard --verbose|snazzy"}
4. 使用编辑器插件，实时检查代码规范
5.git pre-commit 钩子，在每次 commit 之前检查代码规范
```

`bem css` 规范

```js
.person{}
.person__hand{} // hand为子元素或子组件
.person--female{} // person的某一种状态
.person--female__hand{} // 在female状态下的子元素
.person__hand--left{} // 子组件的某一状态
```

