## 1.angularJS 创始人及时间

	Misko Hevery 和 Adam Abrons 于 2009 年 开发
	angularJS 是 一款开源的 JavaScript MV*（MVW、MVVM、MVC）框架
	angularJS 是为了克服 HTML 在构建应用上的不足而设计的

## 2.能干嘛

	·使用 双大括号{{}} 语法 进行 数据绑定
	·使用 DOM 控制结构 来实现 迭代或者隐藏 DOM片段
	·支持 表单 和 表单的验证
	·能将 逻辑代码 关联 到相关的DOM元素上
	·能将 HTML 分组成 可重用的 组件

## 3.如何使用
	
	cnpm i angular   => 取出 angular.js 使用 script链接
	
## 4.四大核心特性

### MVC
	
	高复用 低耦合
	解耦型

	起源：1979年 Trygve Reenskaung 第一次正式提出了 MVC 模式
	好处：职责清晰 代码模块化 便于复用

	M  Model  数据模型层
	V  View   视图层  =>  负责展示 用户看到的界面
	C  Controller  控制器  =>  它是 M 和 V 进行通信的桥梁  （业务逻辑和控制逻辑）

#### MVC 为什么不是 GoF23种设计模式
	
	GoF(Gang of Four，四人组，《Design Patterns: Elements of Reusable Object-Oriented Software》/《设计模式》一书的作者：Erich Gamma、Richard Helm、Ralph Johnson、John Vlissides)并没有把MVC提及为一种设计模式，而是把它当做 "一组用于构建用户界面的类集合"

	在他们看来，它其实是其它三个经典的设计模式的演变：观察者模式(Observer)(Pub/Sub)，策略模式(Strategy)和组合模式(Composite)

	根据MVC在框架中的实现不同可能还会用到工厂模式(Factory)和装饰器(Decorate)模式。

	MVC在核心通讯上基于 推送/订阅模型。
	当一个model变化时它对应其他模块发出更新通知("publishes")，订阅者(subscriber) —— 通常是一个Controller，然后更新对应的 view。观察者 —— 这种自然的观察关系促进了多个view关联到同一个model