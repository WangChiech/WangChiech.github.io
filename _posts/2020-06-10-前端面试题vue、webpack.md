---
layout: post
title: "前端面试题vue、webpack"
subtitle: ''
author: "WangChiech"
header-style: text
tags:
  - 面试

---

## vue基本使用

![image-20200610124916581](\img\image-20200610124916581.png)

![image-20200610124833270](\img\image-20200610124833270.png)

![image-20200610125040911](\img\image-20200610125040911.png)

![image-20200610125230237](\img\image-20200610125230237.png)

![image-20200610125245861](\img\image-20200610125245861.png)

![image-20200610125333901](\img\image-20200610125333901.png)

![image-20200610125358180](\img\image-20200610125358180.png)

v-show	Dom正常渲染，display：none

v-if 不渲染Dom

![image-20200610125722371](\img\image-20200610125722371.png)

![image-20200610125740724](\img\image-20200610125740724.png)

![image-20200610125758852](\img\image-20200610125758852.png)

![image-20200610130338782](\img\image-20200610130338782.png)

![image-20200610130349030](\img\image-20200610130349030.png)

![image-20200610130415529](\img\image-20200610130415529.png)

![image-20200610130943709](\img\image-20200610130943709.png)

![image-20200610130530660](\img\image-20200610130530660.png)

![image-20200610130925200](\img\image-20200610130925200.png)

![image-20200610131248149](\img\image-20200610131248149.png)

![image-20200610132235538](\img\image-20200610132235538.png)

![image-20200610132247754](\img\image-20200610132247754.png)

![image-20200610132311299](\img\image-20200610132311299.png)

![image-20200610134444295](\img\image-20200610134444295.png)

![image-20200610134348412](\img\image-20200610134348412.png)

- created把vue的实例初始化了，只是存在js内存模型中的变量而已，并没有开始渲染
- mounted 组件在页面绘制完成了
- beforeDestroy: 解除绑定、销毁子组件以及事件监听

![image-20200610133054260](\img\image-20200610133054260.png)

![image-20200610134043742](\img\image-20200610134043742.png)

![image-20200610134520482](\img\image-20200610134520482.png)

https://zhuanlan.zhihu.com/p/145168800?utm_source=wechat_session&utm_medium=social&utm_oi=963005880376193024

![image-20200610134851900](\img\image-20200610134851900.png)

- v-model

  ![image-20200610140354290](\img\image-20200610140354290.png)

![image-20200610140547899](\img\image-20200610140547899.png)

![image-20200610140904970](\img\image-20200610140904970.png)

![image-20200610141015245](\img\image-20200610141015245.png)

- 基本使用，父组件往子组件插入一段内容

  ![image-20200610141318138](\img\image-20200610141318138.png)

- 作用域插槽

  ![image-20200610141731849](\img\image-20200610141731849.png)

- 具名插槽

  ![image-20200610141859148](\img\image-20200610141859148.png)

![image-20200610142441827](\img\image-20200610142441827.png)

![image-20200610142559760](\img\image-20200610142559760.png)

![image-20200610142713676](\img\image-20200610142713676.png)

![image-20200610142854119](\img\image-20200610142854119.png)

![image-20200610143124434](\img\image-20200610143124434.png)

![image-20200610143441297](\img\image-20200610143441297.png)

![image-20200610143629107](\img\image-20200610143629107.png)

![image-20200610144107546](\img\image-20200610144107546.png)

![image-20200610144222715](\img\image-20200610144222715.png)

https://zhuanlan.zhihu.com/p/53491958?utm_source=wechat_session&utm_medium=social&utm_oi=963005880376193024

![image-20200610150157409](\img\image-20200610150157409.png)

![image-20200610150207186](\img\image-20200610150207186.png)

![image-20200610150254377](\img\image-20200610150254377.png)

https://juejin.im/post/58fffc52a22b9d0065b8db53

![image-20200610152405215](\img\image-20200610152405215.png)

![image-20200610152444662](\img\image-20200610152444662.png)

![image-20200610152554165](\img\image-20200610152554165.png)

![image-20200610152610232](\img\image-20200610152610232.png)

![image-20200610152700340](\img\image-20200610152700340.png)

![image-20200610154518471](\img\image-20200610154518471.png)

![image-20200610155048350](\img\image-20200610155048350.png)

![image-20200610155143558](\img\image-20200610155143558.png)

![image-20200610155829102](\img\image-20200610155829102.png)

![image-20200610155846472](\img\image-20200610155846472.png)

![image-20200610161156815](\img\image-20200610161156815.png)

![image-20200610161217112](\img\image-20200610161217112.png)

![image-20200610161230327](\img\image-20200610161230327.png)

![image-20200610161254342](\img\image-20200610161254342.png)

![image-20200610161314645](\img\image-20200610161314645.png)

![image-20200610161917723](\img\image-20200610161917723.png)

![image-20200610162117174](\img\image-20200610162117174.png)

![image-20200610162233261](\img\image-20200610162233261.png)

![image-20200610162326070](\img\image-20200610162326070.png)

![image-20200610162513544](\img\image-20200610162513544.png)

![image-20200610162551725](\img\image-20200610162551725.png)

![image-20200610162721533](\img\image-20200610162721533.png)

![image-20200610163634069](\img\image-20200610163634069.png)

![image-20200610163725157](\img\image-20200610163725157.png)

![image-20200610163829893](\img\image-20200610163829893.png)

![image-20200610163949414](\img\image-20200610163949414.png)

![image-20200610164041432](\img\image-20200610164041432.png)

![image-20200610170713804](\img\image-20200610170713804.png)

![image-20200610170848796](\img\image-20200610170848796.png)

![image-20200610171330860](\img\image-20200610171330860.png)

![image-20200610171402147](\img\image-20200610171402147.png)         

![image-20200610171511860](\img\image-20200610171511860.png)

![image-20200610171610741](\img\image-20200610171610741.png)

![image-20200610172609709](\img\image-20200610172609709.png)

![image-20200610172748420](\img\image-20200610172748420.png)

![image-20200610173105507](\img\image-20200610173105507.png)

![image-20200610173205805](\img\image-20200610173205805.png)

![image-20200610173611243](\img\image-20200610173611243.png)

![image-20200610173913700](\img\image-20200610173913700.png)

![image-20200610173943949](\img\image-20200610173943949.png)

![image-20200610174103170](\img\image-20200610174103170.png)

![image-20200610174116503](\img\image-20200610174116503.png)

![image-20200610174414953](\img\image-20200610174414953.png)

![image-20200610174426180](\img\image-20200610174426180.png)

![image-20200610174651138](\img\image-20200610174651138.png)

![image-20200610174742619](\img\image-20200610174742619.png)

![image-20200610174838379](\img\image-20200610174838379.png)

![image-20200610175048659](\img\image-20200610175048659.png)

![image-20200610175243946](\img\image-20200610175243946.png)

![image-20200610175649024](\img\image-20200610175649024.png)

![image-20200610175816227](\img\image-20200610175816227.png)

## 真题演练

![image-20200610180449490](\img\image-20200610180449490.png)

![image-20200610180518570](\img\image-20200610180518570.png)

![image-20200610180535426](\img\image-20200610180535426.png)

![image-20200610180605843](\img\image-20200610180605843.png)

![image-20200610180633033](E:\WangChiech.github.io\img\image-20200610180633033.png)

![image-20200610180718530](E:\WangChiech.github.io\img\image-20200610180718530.png)

![image-20200610180840345](E:\WangChiech.github.io\img\image-20200610180840345.png)

![image-20200610180856712](E:\WangChiech.github.io\img\image-20200610180856712.png)

![image-20200610181034381](E:\WangChiech.github.io\img\image-20200610181034381.png)

.vue 文件实际上是一个class，类，每次使用其实是对class的实例化

![image-20200610181554801](E:\WangChiech.github.io\img\image-20200610181554801.png)

![image-20200610181632457](E:\WangChiech.github.io\img\image-20200610181632457.png)

![image-20200610181700192](E:\WangChiech.github.io\img\image-20200610181700192.png)

![image-20200610181740024](E:\WangChiech.github.io\img\image-20200610181740024.png)

![image-20200610181748416](E:\WangChiech.github.io\img\image-20200610181748416.png)

![image-20200610181823723](E:\WangChiech.github.io\img\image-20200610181823723.png)

![image-20200610181835882](E:\WangChiech.github.io\img\image-20200610181835882.png)

![image-20200610181859184](E:\WangChiech.github.io\img\image-20200610181859184.png)

![image-20200610181928099](E:\WangChiech.github.io\img\image-20200610181928099.png)

![image-20200610181957018](E:\WangChiech.github.io\img\image-20200610181957018.png)

![image-20200610182045865](E:\WangChiech.github.io\img\image-20200610182045865.png)

![image-20200610182111786](E:\WangChiech.github.io\img\image-20200610182111786.png)

![image-20200610182138008](E:\WangChiech.github.io\img\image-20200610182138008.png)

![image-20200610182155609](E:\WangChiech.github.io\img\image-20200610182155609.png)

![image-20200610182256411](E:\WangChiech.github.io\img\image-20200610182256411.png)

![image-20200610182323540](E:\WangChiech.github.io\img\image-20200610182323540.png)

![image-20200610182356241](E:\WangChiech.github.io\img\image-20200610182356241.png)

![image-20200610182428695](E:\WangChiech.github.io\img\image-20200610182428695.png)

![image-20200610182510304](E:\WangChiech.github.io\img\image-20200610182510304.png)

![image-20200610182546894](E:\WangChiech.github.io\img\image-20200610182546894.png)

![image-20200610182832112](E:\WangChiech.github.io\img\image-20200610182832112.png)

![image-20200610183202082](E:\WangChiech.github.io\img\image-20200610183202082.png)

![image-20200610183237203](E:\WangChiech.github.io\img\image-20200610183237203.png)

![image-20200610184215348](E:\WangChiech.github.io\img\image-20200610184215348.png)

```js
// 创建响应式
function reactive(target = {}) {
    if (typeof target !== 'object' || target == null) {
        // 不是对象或数组，则返回
        return target
    }

    // 代理配置
    const proxyConf = {
        get(target, key, receiver) {
            // 只处理本身（非原型的）属性
            const ownKeys = Reflect.ownKeys(target)
            if (ownKeys.includes(key)) {
                console.log('get', key) // 监听
            }
    
            const result = Reflect.get(target, key, receiver)
        
            // 深度监听
            // 性能如何提升的？
            return reactive(result)
        },
        set(target, key, val, receiver) {
            // 重复的数据，不处理
            if (val === target[key]) {
                return true
            }
    
            const ownKeys = Reflect.ownKeys(target)
            if (ownKeys.includes(key)) {
                console.log('已有的 key', key)
            } else {
                console.log('新增的 key', key)
            }

            const result = Reflect.set(target, key, val, receiver)
            console.log('set', key, val)
            // console.log('result', result) // true
            return result // 是否设置成功
        },
        deleteProperty(target, key) {
            const result = Reflect.deleteProperty(target, key)
            console.log('delete property', key)
            // console.log('result', result) // true
            return result // 是否删除成功
        }
    }

    // 生成代理对象
    const observed = new Proxy(target, proxyConf)
    return observed
}

// 测试数据
const data = {
    name: 'zhangsan',
    age: 20,
    info: {
        city: 'beijing',
        a: {
            b: {
                c: {
                    d: {
                        e: 100
                    }
                }
            }
        }
    }
}

const proxyData = reactive(data)

```

![image-20200610184651960](E:\WangChiech.github.io\img\image-20200610184651960.png) 

![image-20200610185526718](E:\WangChiech.github.io\img\image-20200610185526718.png)