# 内容回顾

## webpack演练
	1、打包单个js
	2、打包多个具有依赖关系的js
	3、打包css
		需要style-loader css-loader
		参考:https://doc.webpack-china.org/loaders/
	4、配置文件
		简化在终端里面输入的很长的指令
	5、初体验插件
		webpack.config.js plugins中，是和entry,module同级
	6、webpack 可以接的一些打包参数
		--progress 查看打包进度
		-p 压缩 webpack自带的压缩插件
		--config 文件名称 : 当我们webpack文件名称不叫webpack.config.js
		--watch 监控源文件是否改变，自动打包生成bundle.js
	
## webpack-dev-server + vue 搭建项目
	1、新建必要的文件和文件夹
	
	
	2、在 App.vue、main.js、webpack.config.dev.js中写代码
		App.vue  hello vue
		main.js
			导入App.vue
			利用Vue框架把App.vue渲染出来
			
		webpack.config.js
			最好拷贝我的
		
	3、使用 html-webpack-plugin + webpack-dev-server 运行项目看到效果
		npm run dev

-------------------

# 今日课程目标

## vue-cli【了解】
	步骤:
		1、安装全局包 
			npm install -g vue-cli cross-env
			
		2、把终端切换到一个非中文目录下(推荐桌面)
		
		3、使用vue-cli指令，生成项目
			vue init webpack-simple vue_demo
			
		4、切换到 vue_demo 根目录，并且使用 cnpm install
		
	工作中如何选择以哪种方式搭建项目
		1、有些可能直接去公司的时候，项目已经搭建起来的
		
		2、如果是新项目，可以自己手工的搭建，或是使用脚手架
		
## 黑马买买买项目
	
### 项目的功能点介绍
	商品列表组件：展示商品
	商品详情组件【东西多】：商品的具体信息
	购物车组件【业务逻辑复杂】:多画图、多写笔记
	下订单组件【简单】
	支付页面【简单】
	登录【简单】
	会员中心【简单】
	
	流程：
		展示商品 ---> 展示详情 ---> 加入购物车 ---> 下订单【需要登录】 ---> 支付【需要登录】---> 会员中心

### 项目使用到的技术
	全家桶：vue+vue-router+vuex 
	jquery插件:导航插件、商品预览、二维码生成插件
	vue的第三方包:
		省市区选择...
		element
		iview

### 项目中的静态资源文件和API文档说明
	静态资源已经写好了，你只需要拷贝，使用vue完成它
	
	API文档，我发发送玩过请求的时候，去查看他
	
### 项目学完要达到的程度
	1、vue+vue-router-vuex 必须掌握
	
	2、jquery的插件，会用即可
	
	3、对我们的电商流程要掌握
	
	4、多敲几遍
	
------------------

## 把项目发布到码云上面去【不是必须的】
	码云的地址:https://gitee.com
	
	发布：使用git
	
------------------

## 在项目中使用静态资源&路由

### 项目中使用静态资源
	步骤:
		1、把我给大家的静态资源拷贝到 src/statics目录下面
		
		2、在main.js中，全局导入我们css，那么到时候，所有的组件都可以使用
			需要使用 style-loader css-loader 来处理 css
			需要使用 file-loader url-loader 来处理 ttf|eot|svg|woff
			在webpack.config.dev.js中配置（见代码）
			
### 在项目中使用路由
	1、集成路由到我们项目中
		参考:https://router.vuejs.org/zh-cn/installation.html
		1.1、安装 vue-router
		1.2、在main.js中导入，并且使用Vue.use(xxx)
		
	2、使用路由，把我们根组件的内容，进行动态切换
		html
			router-link to
			router-view
		
		javascript
			定义组件
			创建路由对象，设置路由规则【需要使用到嵌套路由】
			把创建的路由对象，注入到根实例
			
### 嵌套路由的路由规则如何写?
	需求：当点击了购物商城，需要在layout的中间展现商品列表(goodslist.vue)
	
	步骤:
		1、给我们购物商城添加一个 router-link to="/site/goodslist"
		
		2、在layout中间写 router-view 占位符
		
		3、创建商品列表组件(goodslist.vue)
		
		4、在main.js中设置/site/goodslist 匹配的路由规则

------------------

## layout
	头部
		导航条
		
		
			
	
	中间内容

	底部
	
### 导航条功能实现
	1、去jq22.com找到它
	
	2、把相关的静态资源拷贝到我们项目的statics目录下面
	
	3、安装jquery
	
	4、layout.vue中写代码
	
	5、全局导入jquery
		在webpack.config.dev.js的plugins中设置如下代码
		
		new webpack.ProvidePlugin({
	        $:"jquery",
	        jQuery:"jquery"
	    })

-----------------

## 商品列表页面
	步骤:
		1、先完成静态结构
		
		2、发送网络请求	
			使用axios
			1、把axios绑定到Vue的原型上
			2、给axios设置了baseURL
				axios.defaults.baseURL = "http://39.108.135.214:8899/"
		
		3、完成页面渲染
		
### 使用全局过滤器 + moment 实现时间的过滤
	1、在main.js中定义
		Vue.filter()

### 在项目中集成element(基于Vue)
	参考:http://element.eleme.io/#/zh-CN/component/installation
	1、安装 : element-ui
	
	2、在main.js中导入element-ui和他的样式，并且使用Vue.use(xxx)
		参考:http://element.eleme.io/#/zh-CN/component/quickstart
		
	3、使用
		在哪个地方使用，就拷贝哪个组件的代码
	

------------------

## 今日项目中需要用到的包
	第一次安装:
		包名:style-loader css-loader
		应用场景:在我们main.js中导入全局的样式的时候，用到
		安装方式:cnpm i style-loader css-loader -D
		
	第二次安装:
		包名:file-loader url-loader
		应用场景:导入我们的字体文件（因为我们的静态资源中有ttf）
		安装方式:cnpm i file-loader url-loader -D
		
	第三次安装:
		包名:vue-router
		应用场景：在我们的项目中，需要使用vue-router根据不同的路径，切换不同的组件
		安装方式：cnpm i vue-router -S
		
	第四次安装:
		包名:jquery
		应用场景：在我们项目中，需要使用到jquery的一些插件
		安装方式：cnpm i jquery -S
		
	第五次安装:
		包名:axios
		应用场景:项目中需要请求后台数据
		安装方式：cnpm i axios -S
		
	第六次安装:
		包:moment
		应用场景:项目中需要进行时间格式化的时候
		安装方式：cnpm i moment -S
		
	第七次安装:
		包:element-ui
		应用场景：我们商品列表页面的轮播图
		安装方式:cnpm i element-ui -S