# 内容回顾

## export default
	默认导出，相当于 module.exports = 对象/函数/变量
	
	export default 对象/函数/变量
	
	导入
	import goodslist from './components/goods/goodslist'
	
	总结:
		默认导出，别人导入我们的时候，不同加`{}`
	
## export 
	按需导出
		export const name = "zhangsan"
		export const age = 18
		
		上面的和下面的是相等的
		
		const name = "zhangsan"
		const age = 18
		export {name,age}
	
	按需导入
	import {goodslist} from './components/goods/goodslist'
	
	总结:按需导入，必须加`{}`
	
## import & import from 
	导入js、vue import  xxx from 'xxx'
	
	导入css import 
	
	在单文件组件的style中，导入样式，使用 @import "路径";


## 在我们项目中，导入样式
	main.js中导入，因为我们的样式在项目中所有组件中都需要用到
	
	会遇到问题，主要是我们webpack默认不支持导入 ttf、svg等等，
	找到url-loader去打包它们
	
## 路由
	集成Vue-Router
	1、安装
	2、在main.js中导入，并且使用Vue.use
	
	嵌套路由:
		https://router.vuejs.org/zh-cn/essentials/nested-routes.html

--------------------

# 今日课程目标

## 完成商品列表功能
	步骤:
		1、获取数据
		
		2、渲染
		
		3、实现图片懒加载
		
### 图片懒加载
	vue-lazyload
	参考:
		https://www.cnblogs.com/xyyt/p/7650539.html
		https://github.com/hilongjw/vue-lazyload
		
	使用步骤:
		1、安装
		
		2、在main.js中导入，并且使用Vue.use(xxx)
		
		3、在需要的地方，把图片的src换成 v-lazy即可

--------------------

## 完成商品详情

### 点击商品列表中每一项，跳转到商品详情组件
	步骤:
		1、在goodslist.vue的每一商品地方，通过router-link触发
		
		2、创建goodsinfo.vue，设置路由规则
		
		3、在goodslist.vue中获取商品id 

### 根据商品id，发送请求获取数据
	1、methods定义一个发送请求的方法
		axios
		
	2、created调用刚刚在methods定义的发送网络请求的方法

### 渲染数据
	1、渲染商品信息
		实现放大镜的效果，参考我给你的静态资源文件夹里面的内容
		
		注意点:初始化我们的放大镜的时候，一定要放在网络数据回来之后，最好给他加一个200毫秒的延迟
	
	2、渲染推荐商品
	
	3、渲染商品图册
	

### 在商品介绍和商品评论之间切换
	v-show
	
	动态添加样式:
		https://cn.vuejs.org/v2/guide/class-and-style.html

### 使用iview的图钉，实现滚动时，悬停效果
	官网地址:https://www.iviewui.com
	
	在项目中集成
		参考:https://www.iviewui.com/docs/guide/start
	1、全部集成
		1.1、安装包
		
		1.2、在main.js中导入并且，Vue.use(xxx)
	
	2、按需集成
		https://www.iviewui.com/docs/guide/start#%E6%8C%89%E9%9C%80%E5%BC%95%E7%94%A8
	
		2.1、安装包
		
		2.2、安装一个按需导入的包
			babel-plugin-import
			
		2.3、在项目的根目录下面创建一个.babelrc的配置文件
			(babel的配置文件)，拷贝下面的代码到.babelrc中去
				{
				  "plugins": [["import", {
				    "libraryName": "iview",
				    "libraryDirectory": "src/components"
				  }]]
				}
				
		2.4、在商品详情组件中(goodsinfo.vue)，components注册，我们需要使用的组件 Affix ，然后就可以在goodsinfo.vue中使用了
		
### 组件的注册方式
	参考:https://cn.vuejs.org/v2/guide/components.html#%E5%85%A8%E5%B1%80%E6%B3%A8%E5%86%8C
	
	1、全局注册 Vue.component('组件的名称',{})
		所有的组件中都可以使用
		
	2、局部注册 在组件的script的components中注册
		在哪个组件中注册，只能在哪个组件中使用


### 商品评论

### 实现加载评论内容
	步骤:
		1、发送请求
		
		2、使用element分页组件
			参考:http://element.eleme.io/#/zh-CN/component/pagination

### 提交评论
	步骤:
		1、获取到评论的内容
			document.getElementById
			$
			双向数据绑定
			
			refs
				如果真的需要在我们的Vue中操作dom，推荐使用ref
		
		2、发送ajax请求
		
		3、提交完毕之后，清空文本框内容，重新加载第一页的数据

--------------------

### 点击推荐商品，显示对应的商品
	使用watch监控路由的变化，拿到路由中的参数id
	根据路由中的参数id，重新获取数据即可

### 加入购物车动画
	步骤:
		1、获取到加入购物车按钮的位置(left、top)，还要获取购物车徽标所在的位置(left、top)
			$().offset()
			
		2、给我们被动画的元素，加上transition
		
		3、给我们被动画的元素，写样式，写动画的钩子

--------------------

# 今日所安装的包
	第一次安装:
		包名:vue-lazyload
		应用场景:商品列表页面，图片较多，实现懒加载
		安装方式:cnpm i vue-lazyload -S
		
	第二次安装:
		包名:iview
		应用场景:我们商品详情中商品介绍和商品评论悬停功能
		安装方式:cnpm i iview -S
		
	第三次安装:
		包名:babel-plugin-import
		应用场景:按需导入iview/element中的UI组件
		安装方式：cnpm i babel-plugin-import -D
