# Stylus

	Stylus 是一个 CSS 的 预处理框架
		         是一种新型语言
		         可以创建 健壮的、动态的、富有表现力的 CSS
		         默认使用 .styl 的作为文件扩展名，支持多样性的 CSS 语法
		         功能上更为强壮，和 js 联系更加紧密

## CSS 预处理技术

	CSS 预处理技术，是指用一种新语言用来为 CSS 增加可编程的特性，无需考虑 浏览器的兼容性问题
	可以在 CSS 中使用变量、简单的程序逻辑、函数等等在编程语言中的一些基本技巧
	可以让你的 CSS 更加简洁，适应性更强

## Stylus 安装

	npm install stylus -g

## Stylus 简单使用

```.styl
	// src/example.styl
	body,
	html
		background: red
	-pos(type, args)
		i = 0
		position: unquote(type)
		{args[i]}: args[i + 1] is a 'unit' ? args[i + 1] : 0
		{args[i + 1]}: args[i + 1] is a 'unit' ? args[i + 1] : 0
	absolute()
		-pos('absolute', arguments)
	#prompt
		absolute: top 150px left 5px
		width: 200px
		margin-;eft: -(@width / 2)
```

	stylus src/			===> .styl文件  生成  .css 文件
	stylus --compress src/		===> .styl文件 生成压缩的 .css 文件 

```.css
	#propmt {
		position: absolute;
		top: 150px;
		left: 5px;
		width: 200px;
		margin-left: -100px;
	}
```

## $

	Stylus 声明变量没有任何限定，你可以使用 "$" 符号开始
	结尾的分号 (;) 可有可无，但变量名和变量值之间的等号 (=) 是需要的

```.styl
	mainColor = #0982c1
	siteWidth = 1024px
	$borderStyle = dotted
	body
		color mainColor
		border 1px $borderStyle mainColor
		max-width siteWidth
```

```.css
	color: #0982c1;
	border: 1px dotted #0982c1
	max-width: 1024px;
```

## @

	需要注意：
	如果我们使用 "@" 符号开头来声明变量，Stylus 进行编译，但其对应的值并不会赋值给变量
	换句话说，在 Stylus 中不要使用 "@" 符号开头声明变量

## &

	"&" 符号来引用父选择器

```.styl
	ul
		li a
			display: block
			color: blue
			padding: 5px
			html.ie &
				padding: 6px
			&:hover
				color: red
```

```.css
	ul li a {
		display: block;
		color: blue;
		padding: 5px;
	}
	html.ie ul li a {
		padding: 6px;
	}
	ul li a:hover {
		color: red;
	}
```

## @import

	支持导入其他 stylus 样式

## @media

	@media 工作原理和在常规 CSS 中一样，但是，要使用 Stylus 的块级符号

## @
