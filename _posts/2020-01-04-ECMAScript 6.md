---
layout: post
title: "ECMAScript 6"
subtitle: '基于阮一峰 ES6 入门笔记'
author: "WangChiech"
header-style: text
tags:
  - JS
---

[阮一峰ECMAScript 6 入门](http://es6.ruanyifeng.com/#docs/intro)

## 1. let 和 const 命令

### 1-1 let 命令

1. let 声明的变量仅在当前块级作用域内有效。

2. 不存在变量提升（所声明的变量一定要在声明后使用，否则报错）。

3. 暂时性死区，简称 TDZ（区块中`let`和`const`命令，一开始就形成了封闭作用域，在声明之前变量不可用）。

   ```js
   function bar(x = y, y = 2) {
     return [x, y];
   }
   
   bar(); // 报错,参数x默认值等于另一个参数y，而此时y还没有声明
   ```

4. 不允许重复声明(同一作用域)
5. `let`实际上为 JavaScript 新增了块级作用域。

### 1-2 const 命令

1. 声明一个只读的常量 (内存地址不可更改)。
2. 声明的同时必须赋值。
3. 不存在变量提升
4. 暂时性死区
5. 不允许重复声明

> ES6 种声明变量的方法，`var` 、`function` 、`let` 、`const`、 `import`、`class` 

### 1-3 顶层对象的属性

顶层对象，在浏览器环境指的是`window`对象，在 Node 指的是`global`对象。ES5 之中，顶层对象的属性与全局变量是等价的。

- `var`命令和`function`命令声明的全局变量，是顶层对象的属性
- `let`命令、`const`命令、`class`命令声明的全局变量，不属于顶层对象的属性

```js
var a = 1;
// 如果在 Node 的 REPL 环境，可以写成 global.a
// 或者采用通用方法，写成 this.a
window.a // 1

let b = 1;
window.b // undefined
```

### 1-4 globalThis 对象（ES2020)

JavaScript 语言存在一个顶层对象，它提供全局环境（即全局作用域），所有代码都是在这个环境中运行。但是，顶层对象在各种实现里面是不统一的。

- 浏览器里面，顶层对象是`window`，但 Node 和 Web Worker 没有`window`。
- 浏览器和 Web Worker 里面，`self`也指向顶层对象，但是 Node 没有`self`。
- Node 里面，顶层对象是`global`，但其他环境都不支持。

同一段代码为了能够在各种环境，都能取到顶层对象，现在一般是使用`this`变量，但是有局限性。

- 全局环境中，`this`会返回顶层对象。但是，Node 模块和 ES6 模块中，`this`返回的是当前模块。
- 函数里面的`this`，如果函数不是作为对象的方法运行，而是单纯作为函数运行，`this`会指向顶层对象。但是，严格模式下，这时`this`会返回`undefined`。
- 不管是严格模式，还是普通模式，`new Function('return this')()`，总是会返回全局对象。但是，如果浏览器用了 CSP（Content Security Policy，内容安全策略），那么`eval`、`new Function`这些方法都可能无法使用。

综上所述，很难找到一种方法，可以在所有情况下，都取到顶层对象。下面是两种勉强可以使用的方法。

```javascript
// 方法一
(typeof window !== 'undefined'
   ? window
   : (typeof process === 'object' &&
      typeof require === 'function' &&
      typeof global === 'object')
     ? global
     : this);

// 方法二
var getGlobal = function () {
  if (typeof self !== 'undefined') { return self; }
  if (typeof window !== 'undefined') { return window; }
  if (typeof global !== 'undefined') { return global; }
  throw new Error('unable to locate global object');
};
```

[ES2020](https://github.com/tc39/proposal-global) 在语言标准的层面，引入`globalThis`作为顶层对象。也就是说，任何环境下，`globalThis`都是存在的，都可以从它拿到顶层对象，指向全局环境下的`this`。

## 2. 变量的解构赋值

### 2-1 数组的解构赋值

1. 数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值

   ```js
   let [a, b, c] = [1, 2, 3];
   
   let [ , , third] = ["foo", "bar", "baz"];
   third // "baz"
   
   let [x, , y] = [1, 2, 3];
   x // 1
   y // 3
   
   let [head, ...tail] = [1, 2, 3, 4];
   head // 1
   tail // [2, 3, 4]
   
   let [x, y, ...z] = ['a'];
   x // "a"
   y // undefined，如果解构不成功，变量的值就等于undefined
   z // []
   
   /**不完全解构*/ 
   let [a, [b], d] = [1, [2, 3], 4];
   a // 1
   b // 2
   d // 4
   ```

2. 解构赋值允许指定默认值

   ES6 内部使用严格相等运算符（`===`），只有当一个数组成员严格等于`undefined`，默认值才会生效

   ```js
   function f() {
     console.log('aaa');
   }
   let [x = f()] = [1]; // x=1,默认值是一个表达式，那么这个表达式是惰性求值的，即只有在用到的时候，才会求值
   
   let [x = 1, y = x] = [2];    // x=2; y=2,默认值可以引用解构赋值的其他变量，但该变量必须已经声明
   let [x = 1, y = x] = [1, 2]; // x=1; y=2
   let [x = y, y = 1] = [];     // ReferenceError: y is not defined
   ```

### 2-1 对象的解构赋值