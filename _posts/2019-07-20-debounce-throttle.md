---
layout: post
title: "函数防抖、节流"
subtitle: '简单梳理实现方式'
author: "WangChiech"
header-style: text
tags:
  - JavaScript
---

函数防抖和函数节流是防止某一事件在某一事件被频繁触发。函数防抖是某一时间内只执行一次，函数节流是间隔事件内执行。

## 防抖 (debounce)

在规定时间为 n 秒，若两次事件触发时间间隔小于 n 秒，则重新计算函数执行时间

```js
/**
 * @desc 函数防抖
 * @param func 函数
 * @param wait 延迟执行毫秒数
 * @param immediate true 表立即执行，false 表非立即执行
 */
function debounce(func,wait,immediate) {
    let timeout;
    return function () {
        let context = this;
        let args = arguments;

        if (timeout) clearTimeout(timeout);
        if (immediate) { // 立即执行
            let callNow = !timeout;
            timeout = setTimeout(() => {
                timeout = null;
            }, wait)
            if (callNow) func.apply(context, args)
        }
        else { // 非立即执行
            timeout = setTimeout(() => {
                func.apply(context, args)
            }, wait);
        }
    }
}
```



## 节流 (throttle)

在规定时间的间隔内，事件被触发一次。规定时间内反复触发，事件会被合并，但执行时间不会被重新计算。

节流的两种实现方式：

- 时间戳，在时间开始时触发
- 定时器，在时间结束时触发

```js
/**
 * @desc 函数节流
 * @param func 函数
 * @param wait 延迟执行毫秒数
 * @param type 1 表时间戳版，2 表定时器版
 */
function throttle(func, wait ,type) {
    if(type===1){
        let previous = 0;
    }else if(type===2){
        let timeout;
    }
    return function() {
        let context = this;
        let args = arguments;
        if(type===1){ // 时间戳版
            let now = Date.now();

            if (now - previous > wait) {
                func.apply(context, args);
                previous = now;
            }
        }else if(type===2){ // 定时器版
            if (!timeout) {
                timeout = setTimeout(() => {
                    timeout = null;
                    func.apply(context, args)
                }, wait)
            }
        }

    }
}
```

