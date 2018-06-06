# const

    · const 声明一个 只读 的 常量
    · 一旦声明，常量 的值就不能改变
    · const 一旦声明，必须立即 初始化，进行 赋值。否则会 报错
    · 只在声明所在的 块级作用域 内有效
    · 不声明提升，存在 暂存型死区

## 本质

    · const 实际上保证的，并不是变量的值不得改动，而是变量指向的那个 内存地址 不得改动
    · 简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个 内存地址，因此等同于常量
    · 复合类型的数据（主要是 对象 和 数组），变量指向的 内存地址，保存的只是一个 指针，const 只能保证这个 指针是固定的，至于它指向的 数据结构 是不是可变的，就完全不能控制

```.js
    冻结对象 Object.freeze

    const foo = Object.freeze({})
    foo.prop = 123

    foo 指向了一个 冻结的对象，所以添加属性不起作用，严格模式时还会报错
```

```.js
    除了将对象本身冻结，对象的属性也应该冻结。下面是一个将对象彻底冻结的例子

    var constantize = (obj) => {
        Object.freeze(obj)
        Object.keys(obj).forEach((key, i) => {
            if (typeof obj[key] === 'object') {
                constantize(obj[key])
            }
        })
    }
```

## ES6 变量声明的六种方法

    ES5: var function
    ES6: let const import class