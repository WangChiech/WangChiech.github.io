---
layout: post
title: "会话技术"
subtitle: 'cookie、session将数据持久化保存到客户端、服务器端'
author: "WangChiech"
header-style: text
tags:
  - Node.js
---

# 1. 会话技术概况

## 1.1 http协议的缺陷

http是无状态的，就是无记忆，不能让同一浏览器和服务器进行多次数据交换时，产生业务的连续性。

目前，每次请求都是独立的，没有关系的。所以服务器和客户端都不知道是否是登录过的。

## 1.2 什么是会话控制

会话控制就是弥补http无记忆的缺陷的。能够将数据持久化的保存在客户端(浏览器)或者服务器端，从而让浏览器和服务器进行多次数据交换时，产生连续性。



## 1.3 会话控制的分类

- cookie： 将数据持久化保存到**客户端**（浏览器）
- session： 将数据持久化保存到**服务器端**

# 2. cookie技术

## 2.1 什么是cookie

- cookie是将数据持久化存储到客户端的一种技术。

- 网站可以将数据写到浏览器中， 一个网站最多能在一个浏览器写20个cookie。现在的浏览器能写的更多

- 一个浏览器能够设置的总cookie数最多为300个，每个不能超过4kb。

- cookie既能保存在文件中，也能保存在内存中。

- 可以通过浏览器查看某个网站的cookie

    ![1553994777092](\img\1553994777092.png)

## 2.2 设置cookie

- 核心： cookie是服务端设置的，随着响应头返回给浏览器的信息，浏览器要将这些信息记录下来
- 如何设置cookie
  - 使用 res.setHeader
  - 使用res.writeHeader
  - 如果使用的是express框架，可以使用res.set()方法
- cookie设置格式：`key=value;expires=time`
  - key: cookie的名称
  - value： 名称对应的值
  - expires： 有效期

```js
// 所有的设置cookie，都必须写到一个请求中

//1. 使用 http模块中的setHeader 方法，它可以和sendFile一起使用
res.setHeader('set-cookie', 'id=101');                   //设置单个cookie
res.setHeader('set-cookie', ['id=101', 'name=zs']);      //设置多个cookie

//2. 使用 http模块中的writeHeader 方法，它不能和sendFile及send一起使用
res.writeHeader(200, {
    'content-type': 'text/html;charset=utf-8',
    'set-cookie': ['type=10', 'name=my']
})；

//3. 使用 express模块中的set 方法，该方法是express封装的方法，它可以和sendFile一起使用
res.set({'set-cookie':['goodsName=xiaomi 6', 'goodsPrice=3999']})；

//4. 设置cookie时，指定有效期
//注意：要使用UTC时间，使用 toUTCString()方法转换
//设置有效期为 1小时
const expiresTime = new Date(Date.now() + 3600000).toUTCString();
res.set({'set-cookie':['goodsName=xiaomi 6;expires=' + expiresTime, 'goodsPrice=3999']})
```

## 2.3 读取cookie

一旦网站在浏览器设置好cookie之后，浏览器**再访**问网站（任何页面）时，浏览器会将cookie信息随着请求头一起发送给服务器。所以我们在服务器端通过 `req.headers.cookie` 可以获取到cookie的信息。

```js
// 监视浏览器的请求
app.get('/get', (req, res) => {
    // 这里获取cookie
    console.log(req.headers.cookie);
    res.send('你又来了，我上次给你的cookie你带来了吗');
});

app.get('/test', (req, res) => {
    // 这里获取cookie
    console.log(req.headers.cookie);
    res.send('你又来了，我上次给你的cookie你带来了吗');
});

app.get('/test2', (req, res) => {
    // 这里获取cookie
    console.log(req.headers.cookie);
    res.send('你又来了，我上次给你的cookie你带来了吗');
});
```



## 2.4 cookie有效期

- 默认情况是，当关闭浏览器，cookie即消失
- 如果设置了cookie的有效期（expires），则cookie会在指定的有效期内一直存在，无论浏览器是否关闭

```js
// 设置cookie的有效期为1小时
// 方式: 先找到一小时之后的时间戳，再转为utc时间
// Date.now()： 获取当前时间点的时间戳 （毫秒数）
// Date.now() + 3600000： 一小时之后的毫秒数
// new Date(Date.now() + 3600000).toUTCString(): 将时间戳转为时间格式（UTC时间格式）
let time = new Date(Date.now() + 3600000).toUTCString();
// 设置cookie，有效期为1个小时
res.set({
    'set-cookie': ['name=zs;expires='+time]
});
```

# 3. session技术

## 3.1 session介绍

- 因为cookie是保存在客户端的数据，不够安全，所以出现了session。
- session会将数据保存到服务器端（保存在文件、内存服务器或数据表中），安全性就可以得到保证。

## 3.2 设置/读取session

express设置session时，需要使用第三方模块 --- express-session

```shell
npm i express-session
```



使用步骤：

1) 加载 express-session 模块

2) 将session注册为中间件（这样，当有请求过来的时候，都会先经过中间件）

3) 使用 `req.session` 对象设置/读取session

```js
//1. 加载 express-session 模块
const session = require('express-session');
//2. 配置项
let conf = {
    secret: '4ey32erfyf3fgpg',   //加密字符串。 使用该字符串来加密session数据，自定义
    resave: false,               //强制保存session即使它并没有变化
    saveUninitialized: false     //强制将未初始化的session存储。当新建了一个session且未
    							 //设定属性或值时，它就处于未初始化状态。
};
//3. 注册为express-session中间件
app.use(session(conf));

//4. 在一个测试请求中，设置session 
// 方法：  req.session.属性 = 值
app.get('/sets', (req, res) => {
    // session的值可以是任何的数据类型，比如布尔，数组，对象等
    req.session.isLogin = true;
    req.session.userInfo = {user_id:10001, user_name:"zs"};
    //注意：一定要将数据发回给浏览器，否则session无法生效
    res.send('设置session');
});

//设置好之后，req.session中的结构如下，当再次向服务器上任何页面或接口发请求时，我们可以获取到刚刚设置的session值
// req.session = {
//    isLogin: true,
//    userInfo: {user_id:10001, user_name:"zs"}
//}
```

## 3.3 session有效期

- 当服务器关闭后，session消失
- express-session会将session保存在内存中，每次重启服务器时即使没有关闭浏览器session也会消失

> 学习阶段都是开发环境，服务器一会关闭了，一会开启了。
>
> 开发环境中，session是保存在内存中的，所以关闭服务器，session就消失了
>
> 生产环境中session的有效期要设置在配置项中，`cookie: {maxAge: 3600000}`，session应该保存到内存服务器中

## 3.4 删除session

核心： req.session.destroy()    销毁所有session

```js
// 删除所有session
req.session.destroy();
```



## 3.5 session 的有效范围

在一个网站中设置了session，则整个网站都能找到这个session

# 4. cookie、session原理

cookie原理：

![1553999282423](\img\1553999282423.png)

session原理：

服务器端会为每个用户（浏览器）各自保存一个session（文件）

下次用户再来访问的时候，就不能确定该用户的session是哪一个了

所以当服务器保存session之后，会以cookie的形式告诉浏览器，你的session是哪一个

下次再来访问服务器的时候，浏览器就会带着它自己的session号去访问，服务器就可以找到对应的session了

![1553999630174](\img\1553999630174.png)

# 5、cookie和session的优缺点

cookie：优点是节省服务器空间，缺点不安全。

session：优点是安全，缺点需要服务器空间。





