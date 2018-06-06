# create-react-app

是一个全局的命令行工具用来创建一个项目

	如果你正在搭建 react 运行环境，使用 create-react-app 去自动构建你的 app 程序。你的项目所在的文件夹下是没有配置文件的

## 类似这样的脚手架还有

	react-boilerplate
	react-redux-starter-kit
	create-react-app
	
	create-react-app	关注量最大，而且是 facebook 开发

## react-scripts

	是一个生成的项目所需要的开发依赖
	是 facebook 开发的一个管理 create-react-app 服务的工具

	react-scripts 是唯一的额外的构建依赖在你的 package.json 中，你的运行环境将有每一个你需要用来构建一个现代 React app 应用程序
	你需要的依赖，和在配置文件中编写的配置代码，react-scripts 多帮你写了
	还加入了 eslint 的功能

```.html
	// 说明 react-scripts 部分作用
	
	react-scripts 自动下载需要的 webpack-dev-server 依赖
	react-scripts 自己写了一个 nodejs 服务端的脚本代码 start.js 来实例化 WebpackDevServer，并且运行启动了一个使用 express 的 Http 服务器
	
	我们只需要专心写 src 源码就 ok 了，省去了很多精力
```

### react-scripts 有以下支持，都帮你配置好了

	React, JSX, ES6, Flow syntax support
	Language extras beyond ES6 like the object spread operator
	Import CSS and image files directly from JavaScript
	Autoprefixed CSS, so you don’t need -webkit or other prefixes
	A build script to bundle JS, CSS, and images for production, with sourcemaps
	A dev server that lints for common errors

## 线上编译命令

这个是 create-react-app 的一个大亮点，他能让你的应用编译出在线上生产环境运行的代码，编译出来的文件很小，切文件名还带 hash 值，方便我们做 cache，而且他还提供一个服务器，让我们在本地也能看到线上生成环境类似的效果

只需一个命令：
	npm run buld

运行下面两条命令，可以查看线上生产环境的运行效果
	npm install -g pushstate-server
	pushstate-server build

编译好的文件都会放在 build 目录中

## api 开发

在开发 react 应用时，难免与服务器进行数据交互，就是要跟 api 打交道

这时候，有一个问题

api 存在的服务器可能是跟 react 应用完全分开的，而且，开发环境跟线上环境又不太一样

比如，开发环境中，你的 react 应用是跑在 3000 端口的，可是 api 服务可能跑在 3001 端口，这个时候，你跟 api 服务器交互的时候，可能会使用 fetch 或各种请求库，比如 jquery 的 ajax

这个时候可能会遇到 CORS 问题，毕竟端口不同，而线上环境却没有这个问题，因为你都控制线上环境的 react 应用和 api 应用，跑在同一个端口上

按照以往思路，解决的方法可能是用环境变量，比如
	const apiBaseUrl = process.env.NODE_ENV === 'development' ? 'localhost:3001' : '/'

但是这样搞起来，还是有些复杂，然而，create-react-app 提供了一个超级简单的方法，只需要在 package.json 文件中，加一个配置项就 ok 了
比如：
	"proxy": "http://localhost:3001/"

至于你用的是 http 的何种请求库，都是一样的，不用改任何代码。这个选项，只对开发环境有效，线上环境还是保持 react应用 和 api 应用同一个端口

## react-dom

## 运行方式
	
	运行应用程序：
		npm run start
		yarn start
	在浏览器中打开：
		http://localhost:3000

## 生成的目录结构

```.html

	my-app/
		README.md
		node_modules/
		package.json
		.gitignore
		public/
			favicon.ico
			index.html
		src/
			App.css
			App.js
			App.test.js
			index.css
			index.js
			logo.svg

```

### 看 my-app 文件夹下的 public/index.html 和 src/index.js 的源码

可以在这里编写项目代码

```.html
	// 注意：
	
	public/index.html 是启动 http 服务器的首页
	src/index.js 是编译的入口文件
	
	只能叫 index 这个名字，改别的名字不 ok
```

### 打开 http://localhost:3000/index.html 首页

f12 查看网页源码时，我们会看到

```.html
	<script type="text/javascript" src="/static/js/bundle.js"></script>
```

在我们的项目 my-app 中是看不到 /static/js/bundle.js 这个路径的，而我们也并没有写配置文件 webpack.config.js
http 服务器配置，自动打开浏览器窗口，react，es6语法编译，babel-core，webpack，等等这些 你都没有下载，配置
这些活都是由 react-scripts 帮忙做的

## 搭建好运行环境，开发 app

### 导入组件

	由于 babel 依赖，这个项目支持 es6 模块
	当你仍然使用 require() and module.exports，我们鼓励你去使用 import and export 替代

### 增加样式

### Autoprefixer

	react-scripts 通过 Autoprefixer 帮你的 css 文件自动添加浏览器兼容前缀

### 增加 CSS 预处理器

	我比较推荐使用 stylus

首先在 my-app/ 目录下 安装 node-sass 用来将 scss 编译成 css

```.html
	npm install node-sass-save-dev
```

打开 my-app/package.json 增加以下代码到 scripts 中

```.json
	"scripts": {
		"build-css": "node-sass src/ -o src/",
		"watch-css": "npm run build-css && node-sass src/ -o src/ --watch",
		"start": "react-scripts start",
		"build": "react-scripts build",
		....
	}
```

现在你可以重新命名 my-app/src/App.css to my-app/src/App.scss and 运行 npm run watch-css
或者可以改成

```.json
	"scripts": {
		"build-css": "node-sass src/ -o src/",
		"start": "npm run build-css && react-scripts start", // 先执行 build-css 再执行 react-scripts start
		"build": "react-scripts build",
		"test": "react-scripts test --env=jsdom",
		"eject": "react-scripts eject"
	}
```

直接 npm run start

### 增加图片

	当项目构建的时候，Webpack 将正确的移动图片到构建的文件夹下，提供我们正确的路径

```.js
	import React from 'react'
	import logo from './logo.png'	// 告诉 webpack 这个js文件使用这张图片
	
	console.log(logo)	// logo.84287d09.png	// 会改变图片的名字
	
	function Header () {
		// 导入结果是这个图片的 url 地址
		return <img src={logo} alt="Logo" />
	}
	
	export default Header
```

在 css 工作中的方式也一样

```.css
	.Logo {
		background-image: url(./logo.png)
	}
```

webpack 发现所有的相对模块，以 ./ 开始

### 增加 bootstrap

	在 react+es6 moudle+bootstrap
	你不是一定要 React Bootstrap 和 React 一起使用，但是他是流行的库去整合 bootstrap 和 react 应用程序，如果你需要他你可以通过 Create React App 整合他，通过以下几个步骤

```.html
	1、首先安装 React Bootstrap and Bootstrap 从 npm
	   Reac Bootstrap 不包括 Bootstrap CSS，所以你需要去安装
	         在 my-app/ 目录下 安装
	
	npm install react-bootstrap --save
	npm install bootstrap@3 --save
```  

```.html
	2、修改 my-app/src/index.js
	       在你的 src/index.js 文件内容的顶部，导入 Bootstrap CSS 和 可选的 Bootstrap theme CSS
	
	import React from 'react'
	import ReactDOM from 'react-dom'
	import 'bootstrap/dist/css/bootstrap.css'	// 必须
	import 'bootstrap/dist/css/bootstrap.theme.css'	// 可选
	import App from './App'
	import './index.css'
	
	ReactDOM.render(
		<App />,
		document.getElementById('root')
	)
```

```.html
	3、修改 my-app/src/App.js
	
	import React, { Component } from 'react'
	import { Grid, Navbar, Jumbotron, Button } from 'react-bootstrap'
	
	class App extends Component {
		render () {
			return (
				<div>
					<Navbar inverse fixedTop>
						<Grid>
							<Navbar.Header>
								<Navbar.Brand>
									<a href="/">React App</a>
								</Navbar.Brand>
								<Navbar.Toggle />
							</Navbar.Header>
						</Grid>
					</Navbar>
					<Jumbotron>
						<Grid>
							<h1>Welcome to React</h1>
							<p>
								<Button
									bsStyle="success"
									bsSize="large"
									href="http://react-bootstrap.github.io/components.html"
									target="_blank">
									View React Bootstrap Docs
								></Button>
							</p>
						</Grid>
					</Jumbotron>
				</div>
			)
		}
	}
	
	export default App
```

### 最后 运行

	npm run start

