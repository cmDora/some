# global

ES5 的 顶层对象，本身也是个问题，因为它在各种实现里面是不统一的

    · 浏览器 顶层对象 window。Node、Web Worker 没有 window
    · 浏览器 和 Web Worker 里面，self 指向 顶层对象。Node 没有 self
    · Node 里面，顶层对象 global。但 其他环境 都 不支持

    · 全局环境中，this 返回顶层对象。Node、ES6中，this 返回的是当前模块
    · 函数里面的 this，如果函数不是作为对象的方法运行，而是单纯作为函数运行，this指向顶层对象。严格模式下，this返回 undefined
    · 不管是 严格模式，还是 普通模式，new Function('return this')()，总是返回 全局对象。但是，如果浏览器用了 CSP（Content Security Policy，内容安全政策），那么 eval、new Function 这些方法都可能无法使用

## 提案

在 语言标准 的层面，引入 global 作为顶层对象。也就是说，在所有环境下，global 都是存在的，都可以从它拿到顶层对象

垫片库system.global 模拟了这个提案，可以在所有环境拿到 global
```.js
    // CommonJS 的写法
    require('system.global/shim')()

    // ES6 模块的写法
    import shim from 'system.global/shim'
    shim()

    以上代码可以保证各种环境里面，global 对象都是存在的

    // CommonJS 的写法
    var global = require('system.global')()

    // ES6 模块的写法
    import getGlobal from 'system.global'
    const global = getGlobal()

    上面代码将顶层对象放入变量 global
```