# React 数据流

	在 React 中，数据是自顶向下流动的（称为单向数据流），从父组件传递到子组件
	因此组件是简单且易于把握的，它们只需从父节点获取 props 渲染即可
	如果顶层的某个 prop 改变了，React 会递归向下遍历整个组件树，重新渲染所有使用这个属性的组件
	然而在 React 中除了 props 之外还有自己的状态，这些状态只能在组件内修改，就是 state

## props

	就是 properties 的缩写，你可以使用它把任意类型的数据传递给组件（通俗一点就是，可以当成方法传递的参数）

可以在挂载组件的时候设置它的 props

```.js
	import Comment from './comment.js'
	class App extends Component {
		render () {
			var data = {
				name: '程曼',
				title: '标题'
			}
		}
		return (
			<Comment {...data} />
		)
	}

	// comment.js
	// 方法一：
	const Comment = (props) => {

	}

	// 方法二:
	class Comment extends Component {
		render () {
			<div>{this.props.name}</div>
		}
	}
```

当组件内部调用时就是使用 this.props

## propTypes

	propTypes 用于规范 props 的类型与必须的状态
	如果组件定义了 propTypes，那么开发环境下，就会对组件的 props 值的类型做检查
	如果传入的 props 不能与之匹配，React 将实时在控制台里报 warning（警告）

```.js
	static propTypes = {
		// 你可以定义一个 js 原始类型的 prop，默认情况下，这都是可选的
		optionalArray: React.PropTypes.array,
		optionalBool: React.PropTypes.bool,
		optionalFunc: React.PropTypes.func,
		optionalNumber: React.PropTypes.number,
		optionalObject: React.PropTypes.object,
		optionalString: React.PropTypes.string,
		optionalSymbol: React.PropTypes.symbol,

		// 任何可以渲染的东西：数字、字符串、元素 或 数组（或片段）
		optionalNode: React.PropTypes.node,

		// React 元素
		optionalElement: React.PropTypes.element,

		// 你可以声明 prop 是某个类的实例。内部使用的是 JS 的 instanceof 运算符
		optionalMessage: React.PropTypes.instanceOf(Message),

		// 你可以通过将它作为枚举来确保你的 prop 被限制到特定的值
		optionalEnum: React.PropTypes.oneOf(['News', 'Photos']),

		// 可以是许多类型之一的对象
		optionalUnion: React.PropTypes.oneOfType([
			React.PropTypes.string,
			React.PropTypes.number,
			React.PropTypes.instanceOf(Message)
		]),

		// 某种类型的数组
		optionalArrayOf: React.PropTypes.arrayOf(React.PropTypes.number),

		// 具有某种类型的属性值的对象
		optionalObjectOf: React.PropTypes.objectOf(React.PropTypes.number),

		// 采取特定样式的对象
		optionalObjectWithShape: React.PropTypes.shape({
			color: React.PropTypes.string,
			fontSize: React.PropTypes.number
		}),

		// 你可以用 `isRequired` 来连接到上面的任何一个类型，以确保如果没有提供 props 的话会显示一个警告
		requiredFunc: React.PropTypes.func.isRequired,

		// 任何数据类型
		requiredAny: React.PropTypes.any.isRequired,

		// 您还可以指定自定义类型检查器。如果检查失败，它应该返回一个 Error 对象。
		// 不要 `console.warn` 或 throw，因为这不会在 `oneOfType` 内工作
		customProp: function(props, propName, componentName) {
			if (!/matchme/.test(props[propName])) {
				return new Error(
					'Invalid prop `' + propName + '` supplied to' + 
					' `' + componentName + '`. Validation failed.'
				)
			}
		}
	}

	// 以上是 ES6 的写法，如果使用的是 createClass
	MyComponent.propTypes = {
		// 同上
	}
```

## 设置属性默认值

	可以为组件添加 getDefaultProps 和 defaultProps 来设置属性默认值

### getDefaultProps

```.js
	var Comment = React.createClass({
			// 设置默认 props 值
			getDefaultProps: function(){
				name: '默认值'
			},
			render: function() {
				return (
					<div className="Comment">
						{/**接受参数**/}
						{this.props.name}
						{/**接受子节点**/}
						{this.props.children}
					</div>
				)
			}
		})
```

## state

	当前组件内部的数据
	组件本身是一个状态机，他可以在 constructor 中通过 this.state 直接定义他的值，然后根据这些值来渲染不同的 UI
	当 state 的值发生改变时，可以通过 this.setState 方法让组件再次调用 render 方法，来渲染新的 UI

```.js
	
	var Comment = React.createClass({
		// 设置 state 值
		getInitialState: function () {
			num: 0
		},
		addNum: function () {
			var num = ++this.state.num
			this.setState({
				num: num
			})
		},
		render: function () {
			return (
				<div>
					<button onClick={function () {
						this.addNum()
					}}>{this.state.num}</button>
				</div>
			)
		}
	})

	// es6 写法
	class Comment extends Component {
		constructor(props) {
			super(props)
			this.state = {
				num: 0
			}
			this.addNum = this.addNum.bind(this)
		}
		addNum() {
			var num = ++this.state.num
			this.setState({
				num: num
			})
		}
		render() {
			return (
				<div>
					<button onClick={() => {
						this.addNum()
					}}>{this.state.num}</button>
				</div>
			)
		}
	}
```


# 注意

	props 可以访问不可以修改，如果需要修改，请使用 state