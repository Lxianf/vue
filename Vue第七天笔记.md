# 内容回顾

	见截图
	
------------------

# 今日课程目标

## Vuex
	
### 基本概念
	网址:https://vuex.vuejs.org/zh-cn/intro.html
	
	Vuex又称之为 全局 状态/数据 管理，Vuex中的数据，在各个组件
	中都可以操作

### 核心概念【涉及到写代码相关】
	State:要操作的数据
	
	Getter:从仓库中取出数据使用，必须要有返回值
		在需要的地方调用(layout组件中)，写法如下 this.$store.getters.getBuyCount，不能加`()`
		
	Mutation:
		往仓库中增、删、改数据，使用到它
		在需要的地方(商品详情组件中)，通过this.$store.commit('方法名称',载荷/参数)
		
	Action:
	Module:
	
	共同点：
		上面的几个核心概念，它都是对象
	
-------------------

## 商品详情点击加入购物车实现
	存取到我们本地的商品数据的格式，如下
		{商品1的id:数量,商品2的id:数量}
		例如 {"87":5,"94":2}

	步骤:
		1、获取到购买的数量，及该商品的id
			{goodsId:"87",count:3}
			
		2、调用Vuex中mutations中保存商品的方法
			2.1、把vuex集成到我们自己的项目中
				参考:https://vuex.vuejs.org/zh-cn/installation.html
				安装包
				在main.js中导入并且，使用Vue.use(xxx)
				创建一个空白的仓库
				把创建好的仓库，注入到根实例中，那么整个应用就拥有全局存储的功能
				
			2.2、在创建好的空白仓库中，写Vuex的那几个核心概念
				state:要操作的数据，商品的购买总数
				getters:要取的数据，返回的就是购买的商品总数
				mutations:同步的往仓库中增加数据，在这个方法中，最终还是要调用localStorage存储到本地
		
		3、在mutations中保存商品的方法中，调用localStorage保存到本地
			state.buycount = addLocalGoods(goodsObj)
		
		4、在Vuex中的getter中统计localStorage中的总数，给需要的组件
			this.$store.getters.getBuyCount

-------------------

## 购物车【重点、难点】
	购物中，比较麻烦的就是业务逻辑，因为要考虑的东西太多
	
### 发送请求给后台，获取加入购物车中的商品数据

### 渲染商品列表，计算总数量和总价格
	使用计算属性，来统计我们商品的总数量和总价格
	computed
	
	计算属性本质是一个对象，里面就是计算函数，计算函数中必须要return

### 更改商品数量
	父子组件的集成
	
	在购物车父组件中，在展示商品数量的时候，把我们的数量用一个数量选择子组件来呈现
	
	购物车父组件中，包含数量选择子组件

### 如何在父组件中集成子组件
	1、创建一个子组件
	
	2、在父组件中，导入子组件
	
	3、在父组件的components中，注册子组件
	
	4、直接在父组件的template，像自定义标签的形式去使用
	
### 父组件 传值 给 子组件 【通过props】
	参考:https://cn.vuejs.org/v2/guide/components.html#%E4%BD%BF%E7%94%A8-Prop-%E4%BC%A0%E9%80%92%E6%95%B0%E6%8D%AE
	接收方 (inputnumber.vue) 子组件
		子组件要显式地用 props 选项声明它预期的数据：
		props: ['initCount']
		
	发送方 (shopcart.vue) 父组件
		在使用子组件的时候，在子组件的标签中，通过 属性名称=值 的方式，传值
		<inputnumber initCount="1000"></inputnumber>
		
### 子组件 把更改之后的值 传回给父组件 【通过自定义事件】
	参考:https://cn.vuejs.org/v2/guide/components.html#%E8%87%AA%E5%AE%9A%E4%B9%89%E4%BA%8B%E4%BB%B6
	接收方 (shopcart.vue) 父组件
		父组件可以在使用子组件的地方直接用 v-on 来监听子组件触发的事件。
	
	发送方 （inputnumber.vue） 子组件
		通过触发事件传值
		this.$emit('事件名称',值)	 值可以是任何类型
		
### 当子组件中的数量改变之后，重新计算总数量和总价格、更改localStorage中的值
	重新计算总数量和总价格：更改goodsList的值，然后通过计算属性，来计算
	
	调用vuex中 updateGoods 方法 ，Vuex中的方法，调用localStorageTool中的updateLocalGoods

### 删除商品
	调用vuex中 deleteGoodsById 方法 ，Vuex中的方法，调用localStorageTool中的deleteLocalGoodsById

-------------------

## 今日所安装的包
	第一次安装:
		包名:vuex
		应用场景:当我们需要对全局数据进行管理的时候
		安装方式：cnpm i vuex -S
