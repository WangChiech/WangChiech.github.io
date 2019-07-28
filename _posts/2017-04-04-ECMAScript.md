---
layout: post
title: "ECMAScript 知识梳理"
subtitle: 'ECMAScript 详细梳理，定期完善'
author: "WangChiech"
header-style: text
tags:
  - JavaScript
---

## 1.词法结构

该章内容为如何使用 JavaScript 编写程序的基础性规则。作为语法的基础，它规定了诸如变量名是什么、怎么写注释，以及程序语句之间如何分割等规则。

### 1.1 字符集

JavaScript 使用[Unicode]() 字符集编写的。

- JavaScript 才用的是 [UTF-8]() 编写的 Unicode 字符集
- 区分大小写（关键字、变量、函数名和所有标识符）

> UTF-8互联网上使用最广的一种 Unicode 的实现方式
>
> [GB2312]() 简体中文（基本集共收入汉字6763个和非汉字图形字符682个）
>
> [GB5]() 繁体中文
>
> [GBK]() 包括简体、繁体在内的全部中文

### 1.2 注释

```js
// 单行注释内容
```

```js
/**
 * 多行注释内容
 * 多行注释内容
 */
```

### 1.3 直接量

**直接量**(Literals) ，即可以在程序中直接使用的数据

ES5 , ES3 规定的直接量有5种：Null、Boolean、Numeric、String、Regular Expression Literals

在ES3，ES5中，对象和数组被归纳到第十一章（表达式）里，有一个新名词称为 **[初始器]()**（Initialiser）。（*在 JavaScript 高级程序设计与 JavaScript 权威指南中归于直接量*）

### 1.4 标识符与关键字、保留字

**标识符 **就是一个名字，在 JavaScript 中用来对变量、函数命名或用作 JavaScript 代码中某些循环语句的跳转位置标记

- 变量、函数、属性、函数参数的名字
- 第一个字符必须是字母、下划线或 $
- 其他字符可以是字母、下划线、$、数字
- 惯例采用驼峰大小写格式（第一个单词小写，其余单词首字母均大写）
- 标识符中字母也可以包含扩展的 [ASCII]() 或 Unicode 字母字符，但不建议

**关键字、保留字** JavaScript 把一些标识符拿出来用作自己的关键字、保留字。因此，这些字就不能再程序中用作标识符。

ECMAScript 的全部关键字（*为第5版新增）：

```js
break　　do　　    instanceof　　typeof　　  case　 　else　   　new　　var　　  catch　　 finally　　   return　　  void　　 continue　 for　　switch　 while　　 debugger*　　 function　　this　　 with　　 default　　if　　   throw　　 delete　　    in　　      try　　
```

ECMA-262 中的全部保留字（第3版）：

```js
abstract　　  enum　　    int　　    short　　   boolean　 　export　　interface　　 static　　  byte　　   extends　　 long　　    super　　char　　      final　　   native　　 class      synchronized　float　　    package　　   throws　　  const　　  goto　　    private　　transient　　debugger　　 implements　protected　volatile　　double　　   import　　public
```

保留字可能会作为再版的关键字，如第五版新增的debugger就是第三版的保留字。

第五版中非严格模式下的保留字：

```js
implements　　package　　  public　　interface　　private　　static　　let　　       protected　　yield
```

严格模式下保留字：

```js
implements　　package　　  public　　interface　　private　　static　　let　　       protected　　yield
```

*严格模式下，elvel 和 arguments 也不能作为标识符或属性名，否则会抛出错误。*

注意：let和yield为第5版新增保留字，为保证兼容建议将其作为参考保留字。

### 1.5 可选的分号

JavaScript 使用分号将语句分隔开。有利于增强代码的可读性和整洁性。

JavaScript 会填补分号，但仅在缺少分号就无法正常解析时（该条规则在某些情况出错，如下）

```js
var y = x + f
(a+b).toString() // 第二行的圆括号和第一行组成一个函数调用，变成 var var y = x + f(a+b).toString()
```

个人习惯语句结束后添加分号。

## 2. 值、变量和数据类型

JavaScript 程序的运行，即对值（value）进行操作，得到预期的结果，返回给服务端或是展示在页面上（页面的表现、行为），其核心就是操作值（数据）。对于前端，程序运行所需的值有三个来源，一是通过发请求，服务端给我们返回的数据，二是客户通过表单页输入的数据或 prompt(...) 函数，三是网站表现、行为相关的一些固定数据。在 JavaScript 中，我们将所有值分为 7 种数据类型。这些不同数据类型的值，在程序中一般如何取用：一是以字面量的形式直接参与表达式运算；二是赋值给变量（variable），在后续语句中按需读取或修改。

### 2.1 值

**值**，即数据，前端、后端程序的核心都是对数据的操作。

前端主要业务逻辑是实现：

- 将从服务端获取的数据，以一定逻辑进行处理，并渲染到页面上
- 将通过页面中客户输入而获取到的数据，以一定的逻辑进行处理，并传递给后端

后端主要业务逻辑是实现：

- 将前端发送过来的数据，以一定的逻辑进行处理，并保存到数据库
- 根据前端请求内容，从数据库获取数据，以一定的逻辑处理，并返回给前端

因为前端、后端业务需求侧重点不同，前端更注重于客户的交互，所以导致对数据进行逻辑处理的复杂度与方式选择有所不同，但其本质都是对数据的处理，个人认为不管什么语言，始终都是对业务需求实现的一种工具。

### 2.2 变量

**变量** ，其作用是通过想内存申请空间，保存程序中要使用的值。

- JavaScript 是弱类型（也称为动态类型）语言，即变量可以存储任意类型的值
- 变量作为数据的存储容器，可以跟踪整个程序运行过程中的值的变化，从而管理程序的状态
- 变量同时可以用作常量声明，其值在程序执行过程中一直保持不变（ES6 提供了 const 声明常量，所有ES6 部分，都后续梳理）
  - 常量声明，通常放在程序开头，集中设置值
  - 在 JavaScript 中，常量的变量名用大写表示，多单词之间用下划线 _ 分隔

在 JavaScript 中，变量是没有类型的，只有值才有，接下来看其都有哪些类型。

### 2.3 数据类型

JaveScript 有七种数据类型，number、string、undefined、null、boolean、object 和 symbol （符号，ES6 新增），可以使用 typeof 运算符来检测（null 返回object）。

#### 2.3.1 Number 类型

JavaScript 采用IEEE 754标准定义的 64 位浮点格式表示数字。

**整型** 

字面量格式有如下几种

- 十进制，最基本格式

- 八进制，第一位必须是零，然后是八进制的数字序列（0-7）

  ```js
  var octalNum = 070; // 八进制的 56
  ```

  ※ 八进制直面量，在严格模式下无效，支持该模式的 JavaScript 引擎会抛出错误

- 十六进制，前两位必须是 0x ，后跟十六进制数字（0-9及 A-F），其中A-F 忽略大小写

  ```js
  var hexNum = 0x1f; // 十六进制的 31
  ```

在进行算数运算时，八进制、十六进制都最终被转换成十进制数值

**浮点型** 

该数值中必须包含一个小数点，并且小数点后面必须有一位数字

- 浮点数运算时，会出现精度丢失的情况，建议先转换成整数再参与运算，最终转换成浮点数

  ```js
  console.log(0.1+0.2); // 0.30000000000000004
  ```

  计算机不能识别二进制数据以外的任何数据，在进制之间相互转换，某些数值若该进制无法表示，则会出现精度丢失（如10 / 3是除不尽的）

- 保存浮点数需要的内存空间是保存整数的 2 倍，ECMAScript 会尽可能的将数值转换成整数

  ```js
  var floatNum = 10.0; // 解析为整数 10
  ```

- 对于极大极小值，可以用科学计数法表示

  ```js
  var floatNum = 3.125e7; // 等于 31250000
  ```

**数值范围** 

受内存限制，ECMAScript 并不能保存世界上所有的数值

- 最小值保存在 Number.MIN_VALUE 中，大多数浏览器中，这个值是 5e-324
- 最大值保存在 Number.MAX_VALUE 中，大多数浏览器中，这个值是 1.7976931348623157e+308
- 结果的到的数值查过了这个范围，会自动转成字符 Infinity
  - 正值，转换成 Infinity
  - 负值，转换成-Infinity（红宝书中为 -Infinity ；控制台打印为0）
  - isFinite () 函数，可以检测数值是否位于最大最小值之间

**NaN** 

NaN，即非数值（Not a Number），一个特殊的数值，对于一个期待返回数值的程序，可以防止其报错。

- 任何值和NaN操作都会返回NaN
- NaN 和包括自身在内的任何值都不相等
- isNaN () 函数，可以检测一个值是否 ”不是数值“

**数值转换**

Number () 函数

- 如果传入数值，返回原数值
- 如果传入 Boolean ，true 和 false 分别返回 1和 0
- 如果传入 null ，返回 0
- 如果传入 undefined ，返回NaN
- 如果传入字符串
  - 字符串中只包含数字，返回十进制数字（‘011’ ，前面的 0 忽略）
  - 字符串中包含有效的十六进制格式，将返回同等大小的十进制数值
  - 空字符串，返回 0
  - 如果包含上述以外的字符，返回 NaN
- 如果是对象，则调用对象的 valueOf () 方法，依照前面规则返回值，如果转换结果为NaN，则先调用 toString () 方法，再依照前面规则返回值

parseInt () 函数，相对 Number () 简单，更常用。在转换字符串时，更多是看是否符合数值模式。

- 忽略字符串前面的空格，如果第一个字符不是数值或负号，则返回 NaN

- 如果第一个字符是数字字符，则解析下一个字符，直到解析完所有，或是遇到包括小数点在内的非数字字符，返回解析到的数字

- 可以传第二个参数，作为进制格式说明

  ```js
  var num1 = (''); // NaN
  var num2 = ('  abc123abc') // 123
  var num3 = ('123.123') // 123
  var num3 = ('0AF', 16) // 175
  ```

parseFloat () 函数，与 parseInt () 类似，区别是，会把字符串中第一个小数点当做有效字符

#### 2.3.2 String 类型

字符串，用于表示由 0 或多个 16 位 Unicode 字符组成的字符序列。

ECMAScript 中字符串是不可变的，一旦创建，值就不可以再修改

**转换为字符串** 

1. 对非 null 和 undefined 的值调用 toString () 方法，可以选择传递参数：输出数值的进制数，默认十进制
2. 使用 String () 函数，可以转换任意类型，null 返回 'null' ，undefined 返回 'undefined'

#### 2.3.3 Undefined 类型

该类型只有一个值 undefined，在使用 var 声明变量但并未赋值时，这个变量值就是 undefined。

#### 2.3.4 Null 类型

该类型也只有一个值 null。

null 值表示一个空对象指针，如果定义一个变量准备用来将来保存对象，则可以初始化为 null。

undefined 派生自 null ，ECMA-262 规定相等判对时返回 true

```js
alert(null == undefined) // true
```

#### 2.3.5 Boolean 类型

该类型有两个值 true 、false，区分大小写（True 并非 Boolean 值）。

**转换成布尔值**

调用 Boolean () 函数

- 传入Boolean 类型，返回传入类型
- 传入String，如果为空字符串，返回 false；非空字符串，返回 true
- 传入Number，如果为 0 或 NaN，返回false；非0 或 NaN 数值，返回 true
- 传入Object，任何非null，返回true
- 传入 null，返回 false
- 传入 undefined，返回 false

#### 2.3.6 Object 类型

ECMAScript 中的对象其实就是一组数据和功能的集合，可以通过 new 操作符来穿件对象实例，并为其添加属性和方法。

```js
var o = new Object() 
// Object 为一个函数，它是所有实例对象类型的基础，并且实例对象同样具有它里面的所有方法和属性
```

每个实例对象都具有下列属性和方法

- constructor ：该实例对象的构造函数（constructor）即Object()
- hasOwnProperty(propertyName) ：检测还是实例是否具有某属性，传入的属性名必须是字符串
- isPrototypeOf(Object) ：该实例是否为某个对象的原型
- propertyEnumberable(propertyName) ：该实例对象的某个属性是否是可以通过 for-in 枚举，参数的属性名必须是字符串
- toLocaleString() ：返回对象的字符串表示，该字符串与执行环境地区相对应
- toString() ：返回对象的字符串表示
- valueOf() ：返回对象的字符串、数值、或布尔值表示。通常与 toString() 方法返回值相同

#### 2.3.6 Symbol 类型

接下来的ES6 学习中梳理

## 3. 表达式和运算符

## 4. 语句

## 5. 对象

## 6. 数组

## 7. 函数

