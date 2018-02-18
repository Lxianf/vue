# 内容回顾

## 网络请求

### vue-resource
	步骤:
		1、导入Vue、Vue-Resource Vue.use(VueResource)
		
		2、发送请求(GET、POST、JSONP)
			this.$http.get(url).then(response=>{})
			
			this.$http.post(url,{xx:yy,aa:bb},{emulateJSON:true}).then(response=>{})
			
			this.$http.jsonp(url).then(response=>{})
			
### axios
	步骤:
		1、导入Vue、axios
		
		2、发送GET、POST请求
			axios.get(url).then(response=>{})
			
			axios.post(url,{username:'zhangsan',password:123}).then(response=>{})
			
			axios.post(url,"username=zhangsan&password=123").then(response=>{})


### POST发送请求的方式
	1、application/x-www-form-urlencoded 	username=zhangsan&password=123
	
	2、application/json
		"{'username':'zhangsan','password':123}"

------------------

## 品牌管理-网络版
	新增
	
	模糊查询
	
	删除

## 路由
	作用:在单页面应用中，在不刷新浏览器的情况下，根据不同路径，显示不同的组件
	
	步骤:
		1、前提:导入 vue vue-router
		
		2、html
			2.1、<router-link to="/"></router-link>
			
			2.2、<router-view></router-view>
		
		3、javascript
			3、1 定义组件，不要注册
			
			3.2、创建路由对象，设置路由规则(自动的帮我们注册组件)
			
			3.3、把上一步创建的路由对象，注入到/挂载到根实例中
			

### 路由中传递参数
	目标:
		当我们点击了商品的每一项的时候，跳转到商品详情组件中去，
		并且带上id

	步骤:
		1、在商品详情组件中添加 router-link
		2、定义组件
		3、设置路由规则，如果我们的路径中有参数，必须设置动态路由匹配
		4、在商品详情组件中，通过{{$route.params.goodsId}}

## webpack
	作用:
		打包
		
	核心概念:
		entry：打包的入口
		
		output：打包之后结果
		
		loader：打包非js文件
		
		plugins：让webpack飞起来，更牛逼
		
	前提:
		安装两个全局包
		cnpm i webpack -g
		cnpm i webpack-dev-server -g
		
		检测全局包是否安装成功
			全局包 -v

------------------

# 今日课程目标

## 完成 webpack 实际演练 【webpack】(参考赵达的文章)
	参考:http://zhaoda.net/webpack-handbook/install.html

### webpack 打包一个js文件
	步骤:
		1、先在我们的项目中，编写一个js文件(entry.js)，里面写上代码
		
		2、切换到入口文件所在的目录，使用 webpack 入口文件 输出文件 ，例如 webpack entry.js bundle.js
		
		3、在当前目录下面，创建一个index.html，并且导入bundle.js，最后运行看结果

### webpack 打包两个具有依赖关系的js文件
	步骤:
		1、先在我们项目中，创建两个js文件，一个叫做entry.js 另外一个叫做 module.js文件
			它们之间是有依赖关系的，在entry.js中导入module.js
			
		2、切换到入口文件所在的目录，使用 webpack 入口文件 输出文件 ，例如 webpack entry.js bundle.js
		
		3、在当前目录下面，创建一个index.html，并且导入bundle.js，最后运行看结果

### webpack 打包css文件
	步骤:
		1、先在我们项目中，创建两个js文件和一个css文件，一个叫做entry.js 另外一个叫做 module.js文件,
			还有一个叫做style.css，它们之间是有依赖关系的，在entry.js中导入module.js，在entry.js导入了style.css
			
		2、切换到入口文件所在的目录，使用 webpack 入口文件 输出文件 ，例如 webpack entry.js bundle.js
			注意：这一步会失败，详见下面的解决方案
		
		3、在当前目录下面，创建一个index.html，并且导入bundle.js，最后运行看结果
		
### webpack打包css文件
	参考:https://doc.webpack-china.org/loaders/
	
	需要 style-loader css-loader
	
	步骤:
		1、切换到项目根目录，使用 npm init -y 生成package.json
			注意：项目名称必须合法
	
		2、安装包
			cnpm i style-loader css-loader --save-dev/-D
			注意：加了--save-dev就会在package.json中的devDependencies记录，方便多人协作开发
			
			你的小伙伴，如果需要安装项目中所依赖的包，只需要把我们源代码下载下来，切换到根目录，然后使用cnpm install，就会去找package.json中的devDependencies，并且把需要的包安装好
			
		3、在使用webpack打包entry.js的时候，当打包到style.css会报错，这个时候有两种解决方案
			方案1：在entry.js中导入css的时候，在它前面加上 !style-loader!css-loader!
			方案2：可以不用在entry.js中导入css的时候，在它前面加上 !style-loader!css-loader!，在终端打包的时候
			输入如下指令: webpack entry.js bundle.js --module-bind "css=style-loader!css-loader"
			
		4、注意点：
			更改了源文件，一定要把bundle.js删掉，重新打包

### webpack 的配置文件【webpack.config.js】
	作用：大大的简化我们的打包操作
	
	目的：将下面在中端中输入的很长的指令，把它们写在一个叫做webpack.config.js的文件中
		webpack entry.js bundle.js --module-bind "css=style-loader!css-loader&png=url-loader&vue=vue-loader"，然后我在打包的时候，只需要在终端中输入 webpack 打包即可
		
	步骤：
		1、在当前项目的根目录，下面创建一个名称叫做 webpack.config.js 的文件
		
		2、我们在webpack.config.js就写上打包需要的代码【拷贝我的即可】
			entry
			output
			loader
			
		3、切换到项目根目录，在终端中输入 webpack 即可
		
### webpack 插件的初体验
	目的:
		打包出来的bundle.js文件，头部加一个注释
		
	步骤:
		1、安装一个webpack的本地包
			cnpm i webpack -D
			
		2、在webpack.config.js中，导入webpack包，然后设置
			plugins
			注意点：plugins是和 entry、output、module同级

		3、切换到项目根目录，在终端中输入 webpack 即可

### webpack 打包时候可以接的参数
	注意:
		1、打包的时候，我们如果需要额外做一些事情，需要在终端里面，使用webpack打包的时候，
	在webpack后面接一些打包的指令
	
		2、我们webpack打包时候接的参数，没有先后之分，多个之间使用空格隔开即可

	webpack 
		--progress  查看打包进度
		-p  压缩我们打包出来的bundle.js，后面我们选择webpack的压缩插件
		--config webpack配置文件名称 ，比如 --config webpack.config.dev.js
		--watch 监控我们源代码的更改，只要我们源代码改变，就会自动打包

-------------------

## webpack-dev-server + vue构建项目【webpack-dev-server 实现热更新、热重载、热替换】
	目的：一运行项目，在我们的页面上看到Hello Vue，当更改Hello Vue为Hello Girl的时候
	页面上面的内容，在不刷新浏览器的情况下，更新了
	
### 一、先搭建项目的基本结构（建议必要的文件和文件夹）
	 vue_mall_14
	 	|-src
	 	   |-main.js 项目打包的入口文件
	 	   |-App.vue 项目的根组件，项目一启动看到的第一个页面的内容，就写在这里
	 	|-package.json 使用 npm init -y
	 	|-webpack.config.dev.js 开发阶段的webpack配置文件

### 二、在 App.vue、main.js、webpack.config.dev.js中写代码
	1、App.vue 中写 Hello Vue
	
	2、main.js中写代码
		达到的目的就是:
		2.1、导入根组件
			import App from './App.vue'
			
		2.2、渲染根组件
			2.2.1、安装  vue 的包
			2.2.2、创建一个根实例
			2.2.3、使用根实例中的render属性对应的函数，来渲染App.vue到
				id=app的div中去
				
			因为我们打包的是main.js，导入根组件，使用vue实例的render把根组件的
			Hello Vue渲染到id=app的div中去，让用户看到它
			
	3、编写webpack.config.dev.js中的代码
		3.1、安装 vue-loader vue-template-compiler css-loader style-loader 包
		3.2、编写了 entry module
		
### 三、使用 html-webpack-plugin 创建 & webpack-dev-server 打包运行，让用户看到结果
	3.1、使用 html-webpack-plugin 插件 生成 index.html
		3.1.1、安装 html-webpack-plugin webpack webpack-dev-server
		3.1.2、在项目根目录下创建一个参考文件 template.html
			在template中，只需要写id=app的div
		3.1.3、在webpack.config.dev.js中配置plugins
			new HtmlWebpackPlugin({
	            template:'./template.html', //参照文件的路径
	            filename:'index.html'
	        })
		
	
	3.2、在项目的根目录打开终端，在里面输入如下指令
		webpack-dev-server --config webpack.config.dev.js --progress --open --hot --port 6008
		
		我们如果觉得上面比较长，可以把上面一长串指令，可以放在package.json的scripts中，给他添加一个键值对 "dev":webpack-dev-server --config webpack.config.dev.js --progress --open --hot --port 6008，到时候运行，直接在根目录执行 npm run dev
		
		打包bundle.js，并且把生成好的bundle.js和上一步生成的index.html，发布到它内部的node服务器上面去，并且在index.html中，自动导入bundle.js
		
### 总结
	1、先搞明白目的，把vue项目跑起来，实现热更新
	2、我们整个分三大步，第一步(建立必要的文件和文件夹) 第二步（编写上一步生成的文件） 第三步（使用html-webpack-plugin插件和web-dev-server运行项目，看到效果）

------------------

## webpack & webpack-dev-server
	区别之一:
		应用场景不一样:webpack 演练，打包上线的时候用到【生产阶段】
		
		webpack-dev-server : 开发阶段使用，内部自带了一个node服务，可以把我们的代码发布到开启的node，方便开发调试
		
	
	区别之二:
		webpack-dev-server 是在 webpack基础上发展起来的，webpack有的功能webpac-dev-server 基本上都有，并且还比他更加牛逼，webpac-dev-server 它仅仅只能在开发阶段使用
		
	区别之三:
		webpack-dev-server 它不能够在当前我们的项目根目录下生成静态资源文件，所以只适合在开发阶段
		
		webpack 它能够在当前项目根目录下生成静态资源，就可以发布上线了

------------------

## 搭建项目用到的包
	第一次安装:
		包的名称:vue
		应用场景:我们在根组件中去渲染App.vue，需要创建一个根实例，所以需要安装vue这个包
		安装方式: cnpm i vue --save/-S
		
	第二次安装
		包的名称:vue-loader vue-template-compiler css-loader style-loader
		应用场景:在我们webpack.config.dev.js中，需要配置对.vue结尾文件打包支持的时候
		安装方式: cnpm i vue-loader vue-template-compiler css-loader style-loader -D
		
	第三次安装:
		包的名称: html-webpack-plugin webpack webpack-dev-server
		应用场景:在使用html-webpack-plugin生成index.html的使用用到
		安装方式:cnpm i html-webpack-plugin webpack webpack-dev-server -D
		
## 补充其它
	卸载安装错误了的包
		cnpm uninstall vue-loader -D
		
## 任务
	https://vuex.vuejs.org/zh-cn/