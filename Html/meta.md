# meta
所有浏览器都支持 <meta> 标签

## meta 定义 和 用法
	<meta> 元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词
	<meta> 标签位于文档的头部，不包含任何内容。<meta> 标签的属性定义了与文档相关联的名称/值对

## HTML 与 XHTML 之间的差异
	在 HTML 中，<meta> 标签没有结束标签
	在 XHTML 中，<meta> 标签必须被正确地关闭

## 提示 和 注释
	注释：<meta> 标签永远位于 head 元素内部
	注释：元数据总是以 名称/值 的形式被成对的传递的

## 必需的属性
	注意：只有 content 为必需属性
		  http-equiv、name、scheme 为可选属性

### content：定义与 http-equiv 或 name 属性相关的元信息

```.js
	// name 属性主要用于描述网页，与之对应的属性值为 content
	<meta name="参数" content="具体的参数值">
	
	{ // name 主要有以下几种参数：
		1、keywords（关键字）
			说明：用来告诉搜索引擎你网页的关键字是什么
			
		2、description（网站内容描述）
			说明：description 用来告诉搜索引擎你的网站主要内容
			
		3、robots（机器人向导）
			说明：robots 用来告诉搜索机器人哪些页面需要索引，哪些页面不需要索引
			content的参数：content的参数有 all，none，index，noindex，follow，nofollow。默认all
			
		4、author（作者）
			说明：标注网页的作者
			
		5、viewport
			说明：主要是影响移动端页面布局的
			用法：<meta name="viewport" content="width=device-width, initial-scale=1.0">
			注意：width viewport：宽度（数值/device-width）
				 height viewport：高度（数值/device-height）
				 initial-scale：初始缩放比例
				 maximum-scale：最大缩放比例
				 minimum-scale：最小缩放比例
				 user-scalable：是否允许用户缩放（yes/no）
	}
```

### content 中的内容主要是便于搜索引擎机器人查找信息和分类信息用的

### http-equiv

```.js
	// http-equiv 顾名思义，相当于 http 的文件头作用，它可以向浏览器传回一些有用的信息，以帮助正确和精确地显示网页内容，与之对应的属性值为 content，content中的内容其实就是各个参数的变量值
	<meta http-equiv="参数" content="参数变量值">
	
	{ // http-equiv 主要有以下几种参数
		1、Expires（期限）
			说明：可以用于设定网页的到期时间。一旦网页过期，必须到服务器上重新传输
			注意：必须使用 GMT 的时间格式
				  GMT 是格林尼治平时[格林威治标准时间]
				  GMT+8小时，是北京时间
			用法：<meta http-equiv="expires" content="Fri, 12 Jan 2001 18:18:18 GMT">
			
		2、Pragma（cache模式）
			说明：禁止浏览器从本地计算机的缓存中访问页面内容
			用法：<meta http-equiv="Pragma" content="no-cache">
			注意：这样设定，访问者将无法脱机浏览
			
		3、Refresh（刷新）
			说明：自动刷新并指向新页面
			用法：<meta http-equiv="Refresh" content="2;URL=http://www.root.net">(注意后面的引号分别在秒数的前面和网址的后面)
			注意：其中的2是指停留2秒钟后自动刷新到 URL 网址
			
		4、Set-Cookie（cookie设定）
			说明：如果网页过期，那么存盘的 cookie 将被删除
			用法：<meta http-equiv="Set-Cookie" content="cookievalue=xxx;expires=Friday, 12-Jan-2001 18:18:18 GMT;path=/">
			注意：必须使用 GMT 的时间格式
		
		5、Window-target（显示窗口的设定）
			说明：强制页面在当前窗口以独立页面显示
			用法：<meta http-equiv="Window-target" content="_top">
			注意：用来防止别人在框架里调用自己的页面
		
		6、content-Type（显示字符集的设定）
			说明：设定页面使用的字符集
			用法：<meta http-equiv="content-Type" content="text/html; charset=gb2312">
			注意：GB 2312 或 GB2312-80 是中华人民共和国国家标准简体中文字符集
				  GB2312 编码通行于中国大陆；新加坡等地也采用此编码
				    中国大陆几乎所有的中文系统和国际化的软件都支持 GB 2312
				  GB 2312 标准攻收录6763个汉字。其中一级汉字：3755个，二级汉字：3008个
				    它收录的汉子已经覆盖中国大陆 99.75% 的使用频率
				    它对人名、古汉语等方面出现的罕用字和繁体字，并不能处理
				    
		7、content-Language（显示语言的设定）
			用法：<meta http-equiv="Content-Language" content="zh-cn">
			注意：zh-cn：简体中文
				  zh-tw：繁体中文
		
		8、Cache-Control 指定请求和响应遵循的缓存机制
			说明：在请求消息或响应消息中设置 Cache-Control 并不会修改另一个消息处理过程中的缓存处理过程。
			请求时的缓存指令：no-cache、no-store、max-age、max-stale、min-fresh、only-if-cached、max-age
			各个消息中的指令含义：
				Public：指示响应可被缓存区缓存
				Private：指示对于单个用户的整个或部分响应消息，不能被共享缓存处理。这允许服务器仅仅描述当前用户的部分响应消息，此响应消息对于其他用户的请求无效
				no-cache：指示请求或响应消息不能缓存
				no-store：用于防止重要的信息被无意的发布。在请求消息中发送将使得请求和响应消息都不使用缓存
				max-age：指示客户机可以接收响应时间小于当前时间加上指定时间的响应
				max-stale：指示客户机可以接收超出超时期间的响应消息。如果指定 max-stale 消息的值，那么客户机可以接收超出超时期指定值之内的响应消息
	}
```

## meta标签使用技巧

	Meta 标签是用来描述网页属性的一种语言，标准的 Meta 标签可以便于搜索引擎排序，提高搜索引擎网站权重排名。
	要想做的更符合搜索引擎标准就必须了解 meta 标签
	
```.js
	1、Meta 标签的 keywords
		写法：<meta name="Keywords" content="信息参数">
		说明：meta 标签的 Keywords 的信息参数，代表说明网站的关键词是什么
	
	2、Meta 标签的 Description
		写法：<meta name="Description" content="信息参数">
		说明：meta 标签的 Description 的信息参数，代表说明网站的主要内容，概括是什么
	
	3、Meta 标签的 http-equiv=Content-Type content="text/html"
		· http-equiv=Content-Type：代表的是 HTTP 的头部协议，提示浏览器网页的信息
		· <meta http-equiv="Content-Type" content="text/html;charset=信息参数">
		· meta 标签的 charset 的信息参数：GB2312：代表说明网站是采用的编码是简体中文
		· meta 标签的 charset 的信息参数：BIG5：繁体中文
		· meta 标签的 charset 的信息参数：iso-2022-jp：日文
		· meta 标签的 charset 的信息参数：ks_c_5601：韩文
		· meta 标签的 charset 的信息参数：ISO-8859-1：英文
		· meta 标签的 charset 的信息参数：UTF-8：代表世界通用的语言编码
	
	4、Meta 标签的 author
		写法：<meta name="author" content="信息参数">
		说明：meta 标签的 author 的信息参数，代表说明网页版权作者信息
	
	5、Meta 标签的 generator
		写法：<meta name="generator" content="信息参数">
		说明：meta 标签的 generator 的信息参数，代表说明网站采用的什么软件制作
	
	6、Meta标签的 http-equiv="Refresh"
		写法：<meta http-equiv="Refresh" content="时间；Url=网址参数">
		说明：meta 标签的 Refresh 代表多少时间网页自动刷新，加上 Url 中的网址参数代表，多长时间自动链接其他网址
	
	7、Meta 标签的 http-equiv="Pragma" content="no-cache"
		写法：<meta http-equiv="Pragma" content="no-cache">
		说明：代表禁止浏览器从本地计算机的缓存中访问页面内容，这样设定，访问者将无法脱机浏览
	
	8、Meta 标签的 copyright
		写法：<meta name="copyright" content="信息参数">
		说明：meta 标签的 copyright 的信息参数，代表说明网站版权信息
	
	9、Meta标签的 http-equiv="imagetoolbar"
		写法：<meta http-equiv="imagetoolbar" content="false">
		说明：指定是否显示图片工具栏，当为 false 代表不显示，当为 true 代表显示
	
	10、Meta 标签的 Content-Script-Type
		写法： <meta http-equiv="Content-Script-Type" content="text/javascript">
		说明：W3C 网页规范，指明页面中脚本的类型
	
	11、Meta 标签的 revisit-after
		写法：<meta name="revisit-after" content="7 days">
		说明：revisit-after 代表网站重访，7 days 代表7天，依次类推
	
	12、Meta 标签的 Robots
		写法：<meta name="Robots" content="信息参数">
		说明：Robots 代表告诉搜索引擎机器人抓取哪些页面
		其中属性说明如下：
			· 信息参数为 all：文件将被检索，且页面上的链接可以被查询
			· none：文件将不被检索，且页面上的链接不可以被查询
			· index：文件将被检索
			· follow：页面上的链接可以被查询
			· noindex：文件将不被检索，但页面上的链接可以被查询
			· nofollow：文件将被检索，单页面上的链接不可以被查询
```

## 各个浏览器平台的相关 meta 标签的使用

### Microsoft Internet Explorer

```.html
	<!-- 优先使用最新的 ie 版本 -->
		写法：<meta http-equiv="x-ua-compatible" content="ie=edge">
		注意：
			X：在计算机中一般表示 extend，扩展的意思
			UA：User Agent 用户代理
	
	<!-- 是否开启 cleartype 显示效果 -->
		写法：<meta http-equiv="cleartype" content="on">
			 <meta name="skype_toolbar" content="skype_toolbar_parser_compatible">
		注意：
			cleartype：由美国微软公司在其 Windows 操作系统中提供的荧幕字体平滑工具，让 Windows 字体更加漂亮。
					   主要是针对 LCD 液晶 显示器设计，可提高文字的清晰度。
					  基本原理：将显示器的 R G B 各个次像素也发光，让其色调进行微妙调整，可以达到实际分辨率以上（横向分辨率的三倍）的纤细文字的显示效果
					  
```

### Google Chrome
	
```.html
	<!-- 优先使用最新的 chrome 版本 -->
		写法：<meta http-equiv="X-UA-Compatible" content="chrome=1">
		注意：
			<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
			· 这个是 IE8 的专用标记，用来指定 IE8 浏览器去模拟某个特定版本的 IE 浏览器的渲染方式（比如人见人烦的 IE6），以此来解决部分兼容问题，例如模拟 IE7 的具体方式如下：
			  <meta http-equiv="X-UA-Compatible" content="IE=EmulateIE7">
			
			· 而这个标记后面出现了 chrome 的值，不是微软增强了 IE，而是谷歌做了个外挂：Google Chrome Frame（谷歌内嵌浏览器框架GCF）。
			    这个插件可以让用户的 IE 浏览器外表不变，但用户在浏览器网页时，实际上使用的是 Google Chrome 浏览器内核，而且支持 IE6、7、8等多个版本的浏览器
			
			· 安装了 GCF 后，用来指定页面使用 chrome 内核来渲染
			    安装完成后，如果你想对某个页面使用 GCF 进行渲染，只需要在该页面的地址前加上 gcf
			  eg：gcf:http://cooleep.com
			
			· 如果我们想要在开发时指定页面默认首先使用 GCF 进行渲染，如果未安装 GCF 再使用 IE 内核进行渲染，那么就是以下的用法：
			  基本用法：<meta http-equiv="X-UA-Compatible" content="chrome=1"> （用以声明当前页面用 chrome 内核来渲染
			 复杂用法：
			 	· <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"> 
			 	  （这样写可以达到的效果是如果安装了 GCF，则使用 GCF 来渲染页面，如果没有安装，则使用最高版本的 IE 内核进行渲染
			 	· 通过修改 HTTP 头文件的方法来实现让指定的页面使用 GCF 内核进行渲染
			 	    在 HTTP 的头文件中加入以下信息：X-UA-Compatible:chrome=1
			 	    在 Apache 服务器中，确保 mod_headers 和 mod_setenvif 文件可用，然后在 httpd.conf 中加入以下配置信息：{
			 	    	< IfModule mod_setenvif.c >
			 	    	< IfModule mod_headers.c >
			 	    	BrowserMatch chromefram gcf
			 	    	Header append X-UA-Compatible "chrome=1" env=gcf
			 	    }
			 	  在 IIS7 或者更高版本的服务器中，只需修改 web.config 文件，添加如下信息即可：{
			 	  		< configuration >
			 	  		< system.webServer >
			 	  		< httpProtocol >
			 	  		< customHeaders >
			 	  		< add name="X-UA-Compatible" value="chrome=1" />
			 	  		</ customHeaders >
			 	  		</ httpProtocol >
			 	  		</ system.webServer >
			 	  		</ configuration >
			 	  }
	
	<!-- 禁止自动翻译 -->
		写法：<meta http-equiv="google" value="notranslate">
```

### 360 浏览器

```.html
	<!-- 选择使用的浏览器解析内核 -->
	<meta name="renderer" content="webkit|ie-comp|ie-stand">
```

### UC 浏览器

```.html
	<!-- 将屏幕锁屏定在特定方向 -->
		写法：<meta name="screen-orientation" content="landscape/portrait">
	
	<!-- 全屏显示页面 -->
		写法：<meta name="full-screen" content="yes">
	
	<!-- 强制图片显示，即使是"text mode" -->
		写法：<meta name="imagemode" content="force">
	
	<!-- 应用模式，默认将全屏，禁止长按菜单，禁止手势，标准排版，强制图片显示 -->
		写法：<meta name="browsermode" content="application">
	
	<!-- 禁止夜间模式显示 -->
		写法：<meta name="nightmode" content="disable">
	
	<!-- 使用适屏模式显示 -->
		写法：<meta name="layoutmode" content="fitscreen">
	
	<!-- 当页面有太多文字时禁止缩放 -->
		写法：<meta name="wap-font-scale" content="no">
```

### QQ 浏览器

```.html
	<!-- 锁定屏幕在特定方向 -->
		写法：<meta name="x5-orientation" content="landscape/portrait">
	
	<!-- 全屏显示 -->
		写法：<meta name="x5-fullscreen" content="true">
	
	<!-- 页面将以应用模式显示 -->
		写法：<meta name="x5-page-mode" content="app">
```

### Apple iOS

```.html
	<!-- Smart App Banner -->
		写法：<meta name="apple-itunes-app" content="app-id=APP_ID,affiliate-data=AFFILIATE_ID,app-arguments=SOME_TEXT">
	
	<!-- 禁止自动探测并格式化手机号码 -->
		写法：<meta name="format-detection" content="telephone=no">
	
	<!-- Add to Home Screen添加到主屏 -->
	<!-- 是否启用 WebApp 全屏模式 -->
		写法：<meta name="apple-mobile-web-app-capable" content="yes">
	
	<!-- 设置状态栏的背景颜色，只有在"apple-mobile-web-app-capable" content="yes" 生效 -->
		写法：<meta name="apple-mobile-web-app-status-bar-style" content="black">
		
	<!-- 添加到主屏后面的标题 -->
		写法：<meta name="apple-mobile-web-app-title" content="App Title">
```

### Google Android

```.html
	<meta name="theme-color" content="#E64545">
	<!-- 添加到主屏 -->
		写法：<meta name="mobile-web-app-capable" content="yes">
		
	<!-- More info: https://developer.chrome.com/multidevice/android/installtohomescreen -->
```

### App Links

```.html
	<!-- iOS -->
		<meta property="al:ios:url" content="applinks://docs">
		<meta property="al:ios:app_store_id" content="12345">
		<meta property="al:ios:app_name" content="App Links">
	
	<!-- Android -->
		<meta property="al:android:url" content="applinks://docs">
		<meta property="al:android:app_name" content="App Links">
		<meta property="al:android:package" content="org.applinks">
	
	<!-- Web Fallback -->
		<meta property="al:web:url" content="http://applinks.org/documentation">
	
	<!-- More info:http://applinks.org/documentation/ -->
```

## 移动端常用的 meta
	
```.html
	<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no">
	
	<!-- 删除苹果默认的工具栏和菜单栏 -->
	<meta name="apple-mobile-web-app-capable" content="yes">
	
	<!-- 设置苹果工具栏的颜色 -->
	<meta name="apple-mobile-web-app-status-bar-style" content="black">
	
	<!-- 忽略页面中的数字识别为电话，忽略 email 识别 -->
	<meta name="format-detection" content="telephone=no, email=no">
	
	<!-- 启用 360浏览器 的极速模式( webkit ) -->
	<meta name="renderer" content="webkit">
	
	<!-- 避免 IE 使用兼容模式 -->
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	
	<!-- 针对手持设备优化，主要是针对一些老的不识别 viewport 的浏览器，比如黑莓 -->
	<meta name="HandheldFriendly" content="true">
	
	<!-- 微软的老式浏览器 -->
	<meta name="MobileOptimized" content="320">
	
	<!-- UC 强制竖屏 -->
	<meta name="screen-orientation" content="portrait">
	
	<!-- QQ 强制竖屏 -->
	<meta name="x5-orientation" content="portrait">
	
	<!-- UC 强制全屏 -->
	<meta name="full-screen" content="yes">
	
	<!-- QQ 强制全屏 -->
	<meta name="x5-full-screen" content="true">
	
	<!-- UC 应用模式 -->
	<meta name="browsermode" content="application">
	
	<!-- QQ 应用模式 -->
	<meta name="x5-page-mode" content="app">
	
	<!-- windows photo 点击无高光 -->
	<meta name="msapplication-tap-highlight" content="no">
	
	<!-- 适应移动端 end -- >
	
```

# SEO 优化 部分

```.html
	<!-- 页面标题 <title> 标签（head 头部必须）-->
	<title>your title</title>
	
	<!-- 页面关键词 keywords -->
	<meta name="keywords" content="your keywords">
	
	<!-- 页面描述内容 description -->
	<meta name="description" content="your description">
	
	<!-- 定义网页作者 author -->
	<meta name="author" content="author,email,address">
	
	<!-- 定义网页搜索引擎索引方式，robotterms 是一组使用英文逗号 [,] 分割的值，通常有如下几种取值：none，noindex，nofollow，all，index，follow -->
	<meta name="robots" content="index,follow">
```