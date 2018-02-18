# 课程安排

	前面3~4天是基础
	后面8天左右做项目
	
	支付宝:
		open.alipay.com
		
	阿里云:
		https://www.aliyun.com/
		
		使用步骤:
			1、购买阿里云的云虚拟主机 （https://wanwang.aliyun.com/hosting/free?spm=5176.8060947.858673.gongxiangpuhui.250ec835MmatSt）
			
			2、购买域名
				https://wanwang.aliyun.com/?spm=5176.8076989.765261.255.709b4d25ZhUKwJ
				
			3、备案（一定要做）
				推荐下载阿里云App

-------------------

# 今日课程目标

## Vue基本概念的介绍

### Vue是一个什么?
	中文官网:
		https://cn.vuejs.org/
		
	概念:
		渐进式
		JavaScript 框架
		
	特性:
		易用:已经会了 HTML、CSS、JavaScript？即刻阅读指南开始构建应用！
		
		灵活:不断繁荣的生态系统，可以在一个库和一套完整框架之间自如伸缩。
		
		高效:20kB min+gzip 运行大小 超快虚拟 DOM(优化) 最省心的优化
									Diff:http://www.infoq.com/cn/articles/react-dom-diff/
									
	作者:
		https://baike.baidu.com/item/%E5%B0%A4%E9%9B%A8%E6%BA%AA/2281470?fr=aladdin

### Vue能做什么?
	开发Web平台的应用:（最主要的功能）
		PC端:
			网站、后台管理
			
		移动端:WebApp
		
		注意点:只兼容IE9及以上
		
	开发原生平台:
		Weex:可以写js代码开发原生App
		
		原生App（直接运行在Android、iOS操作系统上面）
		
### 如何去学习它?
	看:
		看文档:
			https://cn.vuejs.org/v2/guide/ 【要看】
			https://router.vuejs.org/zh-cn/【要看】
			https://vuex.vuejs.org/zh-cn/【要看】
			https://vue-loader.vuejs.org/zh-cn/（了解）
				实现项目开发时候的热更新/热重载/热替换
		
		第一遍看，概括的看，主要是看它有哪些内容
		
		第二遍看，精读，用到什么就仔细看那一块
		
		第三遍看，工作至少一年，再抽个事件，全部仔细看完
		
	练:
		课程代码【必须】
		https://www.cnblogs.com/8899man/p/6514212.html 【过年敲】
		
	学会查错:
		1、简单的错误，应该一眼能看出来
		
		2、复杂一点的百度(搜索关键字)
		
		3、www.stackoverflow.com

-------------------

## Vue中MVVM

### MVC
	V : View视图，负责拿着数据展现
	C : 调度，把模型数据交给视图去展现
	M : 模型，负责准备好数据
	
### MVVM
	微软 java .net
		javascript actionscript typescript(基于es6)
		es6：http://es6.ruanyifeng.com/
		
	V： View视图，负责拿着数据展现
	VM ： View-Model 相当于Controller
	M：模型，负责准备好数据
	
	好处：
		1. 低耦合。视图（View）可以独立于Model变化和修改，一个ViewModel可以绑定到不同的"View"上，当View变化的时候Model可以不变，当Model变化的时候View也可以不变。

		2. 可重用性。你可以把一些视图逻辑放在一个ViewModel里面，让很多view重用这段视图逻辑。

### Hello Girl(在body的一个p标签中显示 Hello Girl)
	步骤:
		1、导入vue.js
		
		2、写View的代码，写在html的id=app的div中去
		
		3、写View-Model、Model的代码，写在script里面
		
	注意:
		1、我们一个Vue应用，只需要创建一个Vue的根实例
		
		2、我们如果在组件的模版中，如果使用到了指令(比如插值表达式)，必须在我们的模型中，有对应的属性与之对应，否则报错
		
		3、我们的三大框架，都是数据驱动型的框架，一般情况下，我们以后最主要关注的就是模型
		
### CDN【了解】
	CDN的全称是Content Delivery Network，即内容分发网络。
	
	目的:让我们用户访问我们公司网站，WebApp的时候，速度更快
		
-------------------

## Vue中指令
	作用:简化Dom操作
	参考:https://cn.vuejs.org/v2/api/#%E6%8C%87%E4%BB%A4
	
	注意:
		大部分指令都是以v-开头的，并且都是放在标签里面，理解为自定义的属性名称
	
### 插值表达式
	语法:{{}}
	一般内嵌在我们元素里面
	
	注意：可以在我们的{{}}做一些简单的运算或是三目运算符，但是不能写类似于if这种，比较复杂的表达式

### v-text&v-html
	<p v-text="message"></p>
	<p v-html="message"></p>

### v-bind
	使用场景:当我们的页面上显示的值，是动态变化的时候，我们就需要使用到绑定
	比如，我们在页面可能需要换图片
	
	<img v-bind:src="模型中的属性" />
	
	简写
	<img :src="模型中的属性" />
	
	记忆起来，比较麻烦的写法【了解】
	<img v-bind="{src:message}" alt="">

### v-on
	作用:简化事件注册
	
	<button v-on:click="处理函数">点击1</button>
	
	简写，参考:https://cn.vuejs.org/v2/guide/syntax.html
	<button @click="处理函数">点击1</button>
	
	注意点:
		1、我们在使用v-on调用函数的时候，如果函数中没有参数，我们调用的时候，可以加`()`也可以不加，但是如果有参数，就必须加
		
		2、事件它是支持原生事件的，http://www.w3school.com.cn/jsref/jsref_events.asp
		
		3、在methods中，对象里面的事件处理函数，可以使用es6的新语法（简写）
			参考:http://es6.ruanyifeng.com/#docs/object

### v-model
	作用:简化获取表单元素的值
	
	双向数据绑定:
	
	第一条线：从 模型 到 视图
	第二条线：从 视图 到 模型
	
	Vue.js devtools的工具使用
		1、安装
		2、如果你是使用file:// 勾选上允许访问文件网址
		3、不能在生产环境下使用，就是不能导入vue.min.js

### v-if && v-show
	作用：条件渲染，根据条件，显示或是隐藏某些元素
	
	参考:https://cn.vuejs.org/v2/guide/conditional.html
	
	对比:
		v-if，当它为true，创建dom元素，并且显示出来
			  当它为false，删除该dom元素
			  
		v-show，当它为true，显示出来
				当它为false，给它添加一个display:none隐藏起来
				
	应用场景:
		频繁切换，用v-show，如果是一定要到某些条件的时候，才渲染，使用v-if，因为它是惰性的
	
### v-for
	循环，遍历生成元素，遍历数组【最重要】，遍历对象【很少用】
	
	语法:
		<li v-for="item in persons"> 不带索引
		<li v-for="(item,index) in persons"> 带索引
	
	注意点:
		1、你要循环遍历生成什么样的dom元素，就作用于那个dom元素上
		
		2、我们在使用v-for遍历生成dom元素的时候，最好给我们的dom元素，添加一个唯一的key，以此来提高它的效率
		
		3、当我们遍历的时候，来指定key的时候，可以有两种选择，一种是当我们遍历的元素中，有唯一的标识符的时候，我们可以使用每个元素的唯一标识符或是索引，当没有唯一标识符的时候，就用索引
		
### https://cn.vuejs.org/v2/api/#v-cloak

-------------------

## Vue中组件
	一个一个的页面，但是比原先html组件成页面更加强大
	
-------------------

## Vue的过滤器
	作用:对服务器返回的数据进行过滤

-------------------

## 发送网络请求

-------------------

## 补充
	面试题1：
		请你说一下浏览器的兼容性问题，以及解决方案
		
		h5c3之前
			html 没有
			css	不要使用高级的css特性(c3中新东西)
			js jQuery 1.x
			
		h5c3之后
			html html5shiv
			css 浏览器前缀 display:flex
			js 几乎没有
			
	开发建议:
		虽说Vue、React、Angular，推荐我们最好操作数据模型，少操作Dom元素，但是
		该操作还是要操作
	