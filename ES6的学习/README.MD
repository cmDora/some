# ECMAScript 和 JavaScript的关系

    · 1996年11月，JavaScript 的创造者 Netscape 公司
    · ECMAScript 方言还有 Jscript 和 ActionScript
    · ECMAScript 和 JavaScript的关系是：前者是后者的规格，后者是前者的一种实现

# 语法提案的标准流程

任何人都可以向标准委员会（TC39 委员会）提案，要求修改语言标准

### 一种新的语法从 提案 到变成 正式标准，需要经历 五 个阶段。每个阶段的变动都需要 TC39 委员批准

    · Stage 0 -- Strawman（展示阶段）
    · Stage 1 -- Proposal（征求意见阶段）
    · Stage 2 -- Draft（草案阶段）
    · Stage 3 -- Candidate（候选人阶段）
    · Stage 4 -- Finished（定案阶段）

一个提案只要能进入 Stage2，就差不多肯定会包括在以后的正式标准里面
ECMAScript 当前所有的提案，可以在 TC39 的官方网站 Github.com/tc39/ecma262 查看

babel-preset-stage-4 已经整合入 Presets 不单独发布了

# TC39 委员会 

    第 39 号技术专家委员会（Technical Committee 39，简称 TC39）

# Es-Checker

    用来检查各种运行环境对 ES6 的支持情况

    npm install -g es-checker
    es-checker

# Babel 转换器

    Babel是一个广泛使用的 ES6转换器，可以将 ES6/7/8代码 转为 ES5代码，从而在现有环境支持
    （这意味着，你可以用 ES6 的方式编写程序，又不用担心现有环境是否支持）

    学好 babel 必看 ：{
                        https://excaliburhan.com/post/babel-preset-and-plugins.html （如何写好 .babelrc？Babel 的 presets 和 plugins 配置解析）
                        https://segmentfault.com/a/1190000010468759 （Babel 配置项）
                     }

## 如何使用 Babel

    · 第一步就是配置文件 .babelrc 存放在项目的根目录下   ===》  用来设置转码规则和插件
    · 所有 Babel 工具和模块的使用，都必须先写好 .babelrc

```.js
    转换 es2015(es6)的语法，可在 .babelrc 的 plugins 中按需引入 check-es2015-constants 等等几十种不同作用的 plugin。 如下所示：

    // .babelrc

    {
        "plugins": [
            "check-es2015-constants",
            "es2015-arrow-functions",
            "es2015-block-scoped-functions",
            //...
        ]
    }

    Babel 团队为了方便，将同属 ES2015的几十个 Transform Plugins 集合到 babel-preset-es2015 一个 Preset 中，这样你只需要在 .babelrc 的 presets 加入 es2015 一个配置就可以完成全部 ES2015 语法的支持
    
    //.babelrc

    {
        "presets": [
            "es2015"
        ]
    }
```

## 运行Babel

    · plugins 优先于 presets 进行编译
    · plugins 按照数组的 index 增序（从数组第一个到最后一个）进行编译
    · presets 按照数组的 index 倒序（从数组最后一个到第一个）进行编译，因为作者认为大部分会把 presets 写成 ["es2015","stage-0"]

## 转码

presets 字段设定转码规则

### 官方提供规则集

    · 最新转码规则：npm install --save-dev babel-preset-latest
    · react 转码规则：npm install --save-dev babel-preset-react
    · 不同阶段语法提案的转码规则（共有4个阶段），选装一个：{
        npm install --save-dev babel-preset-stage-0
        npm install --save-dev babel-preset-stage-1
        npm install --save-dev babel-preset-stage-2
        npm install --save-dev babel-preset-stage-3
    }

```.js
    //.babelrc

    {
        "presets": [
            "latest",
            "react",
            "stage-2"
        ],
        "plugins": []
    }
```

## 命令行转码 babel-cli

npm install --global babel-cli

```.js
    · 转码结果输出到标准输出
        babel example.js

    · 转码结果写入一个文件
    · --out-file 或 -o 参数指定输出文件
        babel example.js --out-file compiled.js
    · 或者
        babel example.js -o compiled.js

    · 整个目录转码
    · --out-dir 或 -d 参数指定输出目录
        babel src --out-dir lib
    · 或者
        babel src -d lib

    · -s 参数生成 source map 文件
        babel src -d lib -s
```

以上代码实在全局环境下，进行 Babel 转码。
```.js
    坏处：

    · 项目产生了对环境的依赖，因为如果全局环境没有 Babel，就无法运行项目
    · 无法支持不同项目使用不同版本的 Babel
```

```.js
    解决：

    · 将 babel-cli 安装到项目中

        npm install --save-dev babel-cli

    · 改写 package.json

        {
            //...
            "devDependencies": {
                "babel-cli": "^6.0.0"
            },
            "scripts": {
                "build": "babel src -d lib"
            }
        }
    
    · 转码，执行命令

        npm run build
```

## babel-node 

    · babel-cli 工具自带一个 babel-node 命令
    · 提供一个支持 ES6 的 REPL 环境
    · 支持 Node 的 REPL 环境的所有功能，而且可以直接运行 ES6 代码
    · 不用单独包装，随 babel-cli 一起安装
    · 执行 babel-node 就进入 REPL 环境

```.js
    安装在项目中
        npm install --save-dev babel-cli
    
    改写 package.json
        {
            "scripts": {
                "script-name": "babel-node script.js"
            }
        }
```

上面代码中使用 babel-node 替代 node ，这样 script.js 本身就不用做任何转码处理

## babel-register

    · 改写 require 命令。为它加上一个钩子
    · 每当使用 require 加载 .js、.jsx、.es 和 .es6 后缀名的文件，就会先用 Babel 进行转码

```.js
    安装
        npm install --save-dev babel-register
    
    使用（先加载 babel-register）
        require("babel-register")
        require("./index.js")
```

这样就不需要手动对 index.js 进行转码

    注意：

    babel-register 只会对 require 命令加载的文件转码，而不会对当前文件转码。
    由于它是实时转码，所以只适合在开发环境使用

## babel-core

    某些代码需要调用 Babel 的 API 进行转码，就要使用 babel-core 模块

```.js
    安装 
        npm install babel-core --save
    
    调用 babel-core
        var babel = require("babel-core")

        // 字符串转码
        babel-.transform('code();', options)
```

## babel-polyfill 与 babel-runtime 的选择

    问题：
        babel 默认只转换新的 Javascript 语法，而不转换新的 API，比如 Iterator、Generator、Set、Maps、Promise 等等全局对象，以及一些定义在全局对象上的方法（比如 Object.assign）都不会转码

    解决：
        babel-polyfill 与 babel-runtime 就是为了解决这种全局对象或者全局对象方法不足的问题
        {
            当然，你可以用 promise-polyfill 此类 Polyfill 解决全局对象的问题
            或者用 lodash 此类 Utils 解决 Object.assign 这种方法扩展的问题
        }

### babel-polyfill

做法比较暴力，就是将全局对象通通污染一遍

    坏处：
    · 可能会增加很多根本没有用到的 polyfill
    · 可能会污染子模块的局部作用域，严重的或许会导致冲突

    好处：
    · 如果你的运行环境比较low，比如说 Android 一些老机子，而你又需要大量使用 Promise、Object.assign、Array.find 之类的全局对象或者其所属方法，那么使用 babel-polyfill，绝对是一劳永逸

### babel-runtime

相对而言，它的处理方式比较温柔，哪里需要加哪里

    eg：
        需要 Promise 只需：import Promise from 'babel-runtime/core-js/promise'
        （不仅避免污染全局对象，而且可以减少不必要的代码）
           
```.js
    如果多个文件都需要 Promise，则也不需要在各个文件中引入它。只需要使用 babel-plugin-transform-runtime 就可以轻松的帮你省去手动 import 的痛苦，而且它还做了公用方法的抽离，哪怕你有100个模块使用了 Promise，但是 promise 的 polyfill 仅仅存在一份，所有要的地方都是引用一地方

    //.babelrc

    {
        "presets": [
            "env",
            "stage-0"
        ],
        "plugins": [
            "transform-runtime"
        ],
        "comments": false
    }
```

# babel 与 webpack 结合使用

v1 = v1.* ;
v2 = v2.* ;
v3 = v3.* ;

关于 babel 与 webpack 的结合使用 不推荐用 v1，过渡到 v2 或者 v3(推荐) 的版本时，遇到关于 babel 配置的一个问题

```.js
    //.babelrc - webpack v1.*

    {
        "presets": [
            "env",
            "stage-0"
        ]
    }

    //.babelrc - webpack v2.* - v3.*
    
    {
        "presets": [
            ["env", {
                "modules": false
            }],
            "stage-0"
        ]
    }
```

很明显，一眼就能看出相对于 v1.* 的版本，v2.* 或者 v3.* 版本多了 "modules": false 这项配置，如果仔细看了 "https://webpack.js.org/guides/migrating/#mixing-es2015-with-amd-and-commonjs" 官网就明白了。
以前你可能需要 babel 来将 ES6 的模块语法转换为 AMD、CommonJS、UMD 之类的模块化标准语法，但是现在 webpack 已经把这个事情做了，所以就不需要 babel 来做了，但是 babel 配置项中的 modules 默认值是 commonjs，所以你需要将 modules 设置为 false 才行，不然就冲突了