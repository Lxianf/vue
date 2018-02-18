# 内容回顾

## 动画
	我们要动画的元素，必须包裹在 transition

### 第一种:根据vue提供好的类名，我们程序员自己写css样式
	参考:https://cn.vuejs.org/v2/guide/transitions.html
	
### 第二种:可以使用第三方的样式库(animate.css)
	使用注意：
		1、我们要动画dom元素，在遇到inRight，outRight，必须是一个块级元素，并且要设置宽高
		
		2、我们的类名，必须要加上 animated
		
### 第三种:通过我们的Vue提供的动画钩子【自己写css和js】
	使用注意:
		1、我们的被动画的元素，从显示到隐藏的时候，我们在动画离开的时候(leave)一定注意一下
		
		2、当我们在进入过渡期间(enter)和离开过渡期间(leave)，如果发现没有动画想过，要在设置结束位置之前，加上el.offsetWidth/el.offsetHeight这句话

---------------------

## 组件

	可重复使用的模版，最终还是需要呈现出来给用户看，在Vue中还可以认为它是自定义标签
	
### 前四种组件的写法【熟悉，能看得懂文档】
	第一种:先定义，在注册【必须】，最后使用
	第二种:定义和注册一步到位，最后使用
	第三种:对第一种template的优化【template】
	第四种:对第一种template的优化【script】

### 第五种组件的写法---使用单文件组件
	参考:https://cn.vuejs.org/v2/guide/single-file-components.html
	
### 根实例(new 来创建的) 和 组件的比较
	相同点：都是Vue的实例
	
	不同点:
		一个项目中只会有一个根实例，所有它里面的data有两种写法
		data:{} data(){ return {}  }
		
		组件中，data必须是一个函数，但是除了一些根级特有的选项，其它和根实例没有多大的区别

----------------------

## 计算属性和watch
	共同的特点:
		写法上可以用一个`{{}}`来显示结果
		都可以监控 data 中数据的变化
		
	计算属性:
		写在computed中，本质是一个对象，对象中有计算的函数
		计算属性的函数必须return
		调用的时候，和普通的插值表达式一样
		当它所依赖的某个属性值发生更改，都会触发计算属性
		
	watch:
		写在watch中，本质也是一个对象，把我们要监控的模型作为key，处理函数作为值
		
		函数中有两个参数：第一个新值，第二个是旧值

----------------------

## 品牌管理-内存版
	新增:
		
	删除:
		根据id获取当前点击的索引 es6中 findIndex
		
	过滤器:
		私有:
			写在组件的filters，过滤器内部也是一个一个的函数，函数必须接收输入的原始值，过滤之后要把结果return
			
			调用的时候，{{原始数据 | 过滤器函数}}
		
		全局:
			写在组件的前面，Vue.filter('过滤器函数名称',处理函数)
			
			处理函数的写法和私有过滤器一样，调用方式也一样

----------------------

# 今日课程目标

## Vue中发送网络请求
	它是支持 XMLHTTPRequest、jQuery($.ajax())

### vue-resource【基于Vue，只能在Vue中用】
	参考:https://github.com/pagekit/vue-resource
	
	POST请求:
		https://github.com/pagekit/vue-resource/blob/develop/docs/http.md
		
	JSONP请求:
		只要把get方法改成jsonp方法即可
	
### axios【没有基于Vue，在其它框架中都可以使用】
	参考:https://www.awesomes.cn/repo/axios/axios
	https://www.awesomes.cn/repo/axios/axios
	
	使用注意:
		1、注意post提交参数的区别

### vue-resource 和 axios的 区别
	1、vue-resource是基于vue的，只能在vue中使用
	2、axios没有基于Vue，在其它框架中都可以使用
	3、vue-resource支持jsonp，axios不支持
	4、vue-resource不支持在node中使用，axios支持

----------------------------
	
## 完成品牌管理的网络版

### API的说明
	获取列表:http://157.122.54.189:9093/api/getprodlist
	新增:http://157.122.54.189:9093/api/addproduct
	删除:http://157.122.54.189:9093/api/delproduct/42974
	
### Vue实例的生命周期
	注意:
		1、Vue给我们提供了一系列的生命周期钩子(beforeCreated，created...)
		
		2、我们生命周期钩子，只要程序员实现了，Vue就会在恰当的时机调用
		
### 使用计算属性查询用户输入的关键字
	1、在computed中写，在computed中写的都是函数，函数必须要有返回值
	
	2、getnewlist计算属性中有两个return ，作用是不一样的

----------------------------

## 路由
	作用:根据不同的路径，显示不同的组件
	
	单页面应用就要靠路由
	
	参考:https://router.vuejs.org/zh-cn/essentials/getting-started.html

	前提:
		1、导入vue.js
		2、导入vue-router.js

	步骤:
		html中写代码
			1、写触发链接的标签
				<router-link to="/newslist">新闻列表</router-link>
			
			2、路由的占位符
				<router-view></router-view>
		
		javascript中写代码
			1、定义组件【不要注册，下面设置路由规则的时候，会自动把我们的组件注册】
			
			2、创建路由对象，设置路由规则(自动帮我们把组件注册)
			
			3、把我们上一步创建的路由对象，注入到根实例，这样我们整个应用就拥有了路由的功能
			
### 带有路由参数的使用
	需求:
		点击我们商品列表每一项，进入商品详情组件中去，并且带上商品id
		
	实现步骤:
		1、给我们商品列表中的 卫龙辣条、周黑鸭，加上 <router-link to="/goodsinfo/1001"></router-link>
		
		2、定义商品详情组件
		
		3、在跳转过来的商品详情组件中，获取赋值到goodsId上面的真实的值(就是1001、1002)
			参考:https://router.vuejs.org/zh-cn/essentials/dynamic-matching.html

-------------------------
	
## webpack

### 基本概念
	Webpack 是当下最热门的前端资源模块化管理和打包工具。它可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源。还可以将按需加载的模块进行代码分隔，等到实际需要的时候再异步加载。通过 loader 的转换，任何形式的资源都可以视作模块，比如 CommonJs 模块、 AMD 模块、 ES6 模块、CSS、图片、 JSON、Coffeescript、 LESS 等。
	
	
	官网:
		https://webpack.js.org/
		
### 核心概念
	入口(entry)
		打包的入口文件，一般我们把打包的入口文件命名为: main.js
		
	输出(output)
		打包之后，得到的输出的文件，如果做到极致，把所有的源代码都打包进入
		一个 bundle.js 
		
	loader
		打包非.js文件
		参考:https://doc.webpack-china.org/loaders/
		
	插件(plugins)
		让我们webpack更牛逼
		
### 前提准备(安装两个全局包)
	webpack:
		cnpm i webpack -g
		
	webpack-dev-server:
		cnpm i webpack-dev-server -g
		
	如何检测有没有安装成功
		webpack -v
		webpack-dev-server -v

----------------------

## 其它

### es6之箭头函数
	语法:
		const 函数名称 = (形参列表) => {
			方法体
		}
		
	注意点:
		1、如果形参列表中，只有唯一一个形参，可以省略`()`，其它情况，通通不能省略
		
		2、当我们方法体只有一句话的时候，可以把`{}`
		
		3、当我们方法体只有一句话的时候，可以把`{}`，并且当它里面有 return 的时候，要么和`{}`一起省略，要么全都不省略，虽然return 省略，但是值照样会返回
		
		4、我们箭头函数中this的指向不一定指向调用它的对象，所以使用的时候，最好打印一下，确认一下

----------------------