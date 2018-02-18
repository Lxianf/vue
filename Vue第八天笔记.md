# 内容回顾

## 在商品详情页面中，点击加入购物车
	1、动画
	
	2、更改购物车徽标上面值(Vuex)
	
	3、把我们添加到购物车中的商品还需要存储到本地
		localStorage
		最终在localStorage中的存储方式是
		{商品id1:数量,商品id2:数量}
		
## Vuex的基本概念
	全局数据存取的仓库
	
## Vuex的核心概念
	state：要操作数据、商品购买的总数
	getter：从仓库中取数据的时候，取出的也是商品的总数
		调用方式:this.$store.getters.xxx，不要加`()`
	
	motation：往仓库中同步的增、删、改数据
		调用方式:this.$store.commit('函数名称',载荷)
	
	action：往仓库中异步的增、删、改数据
	
	
	module:当需要创建多个仓库的时候，需要用到
	
	注意点:上面的这些都是对象
	
## 在项目中集成Vuex
	1、安装包
	2、在main.js中导入并且，Vue.use(Vuex)
	3、创建一个空白的仓库
		参考:https://vuex.vuejs.org/zh-cn/getting-started.html
	4、一定要把创建好的空白仓库注入到根实例中【不能少】
	
	5、state:{
		 buycount:0
	   }
	   
	6、mutations:{
		addObj(state,goodsObj){
		}
	}

## 购物车的组件
	1、把加入到购物车中的组件展示出来
		1.0、把需要发送请求的id，从localStorage中取出来
		1.1、发送请求 axios
		1.2、对服务器返回的数据进行处理
			给我们每一行数据加上buycount
			给我们的每一行加上isSelected用于开关控制
	
	2、统计商品的总数量和商品的总价格
		计算属性
	
	3、更新商品的数量
		父组件集成子组件
			在父组件中导入子组件
			在父组件的components中注册
			在父组件的template中像自定义标签一样使用
		
		父组件 传值给 子组件【通过props】
			接收方（子组件inputnumber.vue）
				子组件要显式地用 props 选项声明它预期的数据：
			
			发送方（父组件shopcart.vue）
				在使用子组件的地方，通过子组件的标签中，通过属性名称=值
		
		子组件 传值给 父组件【通过自定义事件】
			接收方（父组件shopcart.vue）
				父组件可以在使用子组件的地方直接用 v-on 来监听子组件触发的事件。
				
			发送方（子组件inputnumber.vue）
				this.$emit('自定义事件名称',值)
	
	4、删除商品

-----------------------

# 今日课程目标

## 编程式导航
	在购物车组件中，点击了`继续购物`按钮之后，跳转到商品列表
	
	
## 声明式导航 & 编程式导航
	相同点:都能进行导航，实现页面间跳转，并且带上参数
	
	
	不同点:
		写法不一样：
			声明式导航，是写在组件的template之间的，写法如下
			<router-link to="/xx/yy"></router-link>
			
			<router-link :to="'/xx/yy/'+item.id"></router-link>
			
			编程式导航，是写在script里面，写法如下
			this.$router.push()
			this.$router.go()
			
## 编程式导航中 $router.push中可以带的参数说明
	没有带参数
		this.$router.push({path:'/site/goodslist'})
		path是和我们设置路由规则时候的path一致就行了
		
		this.$router.push({name:'goodslist'})
		name就是命令路由
		
	带参数:
		第一种方式:params
			this.$router.push({path:'/site/goodsinfo/xxx/yyy'})
			
			在渲染出来的组件中获取值
				this.$route.params.xxx
				this.$route.params.yyy
				
		第二种方式:query
			this.$router.push({path:'/site/goodsinfo',query:{xxx:'111',yyy:'333'}})
			
			在渲染出来的组件中获取值
				this.$route.query.xxx
				this.$route.query.yyy
				
	开发中建议:
		不需要纠结究竟用哪种，你爱用哪种，就用哪种，但是要把组件渲染出来，并且如果有参数
		还需要带上对应的参数
		
### $router && $route
	相同点：
		1、都是属于vue-router里面的
		2、必须要在集成vue-router的时候，使用Vue.use(VueRouter)，才会在vue原型
		上面绑定$route、$router这两个属性
		
	不同点:
		1、$router是在编程式导航的时候，使用到它，它里面有两个方法 $router.push、$router.go
		
		2、$route 用来获取路劲中的参数，$route.params.xxx，还可以通过 $route.query.xxx来获取路径中的参数 
			在监控路径变化的时候，使用到它

-----------------------

## 登录【逻辑有点绕】

### 登录需要做的事情
	1、我们跳转到有些组件中，有些是需要权限，有些是不需要权限
		不需要登录就能访问的组件如下:
			商品列表(goodslist.vue)
			商品详情(goodsinfo.vue)
			购物车(shopcart.vue)
			
		需要登录:
			下订单组件
			支付组件
			会员中心
	
	2、当我们要跳转到需要登录的组件中的时候，如果你没有登录，先跳转到登录页面
	登录完成之后，再跳转到你需要的那个组件中去
		2.1、给我们需要登录之后，才能访问的组件的路由规则上面加上一个元数据/元信息
			{path:'order/:ids',component:order,meta:{needLogin:true}}
			
		2.2、利用导航守卫来判断哪些是需要做权限校验，哪些是不需要的，如果需要做权限验证
		需要发送请求给后台，如果后台返回的结果是已登录，直接调用next跳过去，如果后台返回是没有登录，跳转到登录组件，进行登录
			注意点:如果发送请求用的axios axios.defaults.withCredentials = true 必须设置为true
	
	3、登录/登出完成之后，还需要更新我们layout组件头部里面的登录&注册 会员中心&退出
	
	4、把我们登录/登出之后的状态保存在本地

### 导航守卫
	参考:https://router.vuejs.org/zh-cn/advanced/navigation-guards.html
	
### axios
	axios.defaults.withCredentials = true

-----------------------

## 非父子组件通讯
	1、搞一个公共的Vue实例【前提】
	
	2、在发送方，通过bus.$emit()触发事件，传值
	
	3、在接收方，通过bus.$on('事件名称',function(值){
		//获取到值，进行操作
	})

	注意点:
		在非父子组件中，在接收方的处理函数中，要想里面的this指向组件的Vue实例，有三种解决方案
		方法1：在外面定义一个变量
			const _this = this
			
		方式2：通过bind
			
		方式3：箭头函数
		

-----------------------

## Vue组件的生命周期

### 基本概念
	Vue组件的生命周期和人的生命周期有些相似
	
	人: 出生 ---> 上学 ---> 工作 ---> 结婚 ---> 过上幸福的生活 ---> 挂了
	
	Vue:
		beforeCreate（组件创建之前） ---> created（组件已经创建出来了）
		---> beforeMount（组件的dom元素被渲染出来之前） ---> mounted（dom元素已经渲染出来了） ---> 【模型数据发生了更改】beforeUpdate（视图重新渲染之前） ---> updated(视图已经重新渲染完毕) ---> beforeDestory(组件销毁之前) ---> destoryed（组件销毁了）

### 注意点:
	1、Vue的一系列生命周期钩子，都是Vue框架提供者，我们开发者，只需要
	实现，那么我们Vue框架底层就会在恰当的时机，自动调用他们
	
	2、每个组件中都有这些生命周期钩子
	
### 应用场景:
	1、created
		发送网络请求
		
	2、mounted
		等视图渲染完成，然后拿着dom进行操作，有时候可能还需要加载写延时
		
	3、beforeUpdate & update
		数据模型发生了更改，会调用，它会重新渲染组件
		
	4、beforeDestory & destory
		beforeDestory 记录未提交的数据
		created 将本地的数据，自动填充上
		
		beforeDestory:记录上次滚动到那个地方了
		created：自动滚动到你上次看得那个位置

-----------------------