# jsx

	· 在 react 中 jsx 只作为转义语言使用
	· jsx 执行返回的结果就是虚拟 dom ，一个 js 对象树
	· 在 jsx 中，class 需要替换成 className，label 元素的 for 属性需要替换成 htmlFor
	· Babel 转译器会把 JSX 转换成一个名为 React.createElement() 的方法调用

## jsx 写法

	· react 把 html 写到 js 当中，这种写法称为 JSX
	· 是一种类似 XML 的写法，他可以定义类似 HTML 一样简洁的树状结构
	· 这种语法结合了 JavaScript 语法 和 HTML 的优点，既可以像平常一样使用 HTML，也可以在里面套 JavaScript 语法
	· 这种友好的格式，让开发者 易于阅读 和 开发

### 注意

	· JSX 和 HTML 完全不是一回事，JSX 只是作为 编辑器，把类似 HTML 的结构编译成 JavaScript
	· 在浏览器中不能使用直接使用这种格式，需要添加 JSX 编译器来完成这项工作

## 基本语法

使用 类XML 语法的好处是标签可以任意嵌套，我们可以像 HTML 一样清晰地看到 DOM 树状结构及其属性。

```.jsx
	const List = () => (
		<ul>
			<li>列表元素1</li>
			<li>列表元素2</li>
			<li>列表元素3</li>
			<li>列表元素4</li>
		</ul>
	)
```

写这个组件的过程就像写 html 一样，只不过它被包裹在 JavaScript 的方法中，需要注意以下几点

	· 定义标签时，只允许被一个标签包裹
	· 标签一定要闭合