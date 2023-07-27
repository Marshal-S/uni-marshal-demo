<template>
	<view class="container">
		<text>本项目已包含uni ui组件，无需import和注册，可直接使用。在代码区键入字母u，即可通过代码助手列出所有可用组件。光标置于组件名称处按F1，即可查看组件文档。</text>
		<dy-double-button :name="dName" :age="dAge" @valueChanged="onComponentChanged" />
		<dy-double-button :name="dName" :age="dAge" desc="哈哈哈哈" @valueChanged="onComponentChanged" />
		<dy-double-button :name="name" :age="age" :desc="desc" @valueChanged="onComponentChanged">
			<text>我是内嵌入的节点</text>
		</dy-double-button>
		<text>总年龄：{{totolAge}}</text>
		<text>平均年龄：{{averageAge}}</text>
		<text>我是{{stu.name}}</text>
		<view @click="onUpdateName">点击我从外部更新desc</view>
		<my-button />
		<view @click="goOrder">点击进入my-order</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				dName: 'marshal',
				dAge: 20,
				
				count: 0,
				name: 'marshal绑定',
				desc: '',
				age: 40,
				stu: {
					name: '小刘'
				}
			}
		},
		computed: {
			//直接编写的的是get方法
			averageAge() {
				return (this.dAge + this.age) / 2
			},
			//可以分开定义set和get方法
			totolAge: {
				get() {
					return this.dAge + this.age
				},
				set(newVal) {
					let half =  newVal / 2 
					this.dAge = half
					this.age = newVal - half
				}
			},
		},
		//推荐
		mounted() {
			// 渲染之后调用，一般逻辑在这里，调用一次
			console.log('mounted')
		},
		//h5使用
		activated() {
			// keep-alive 缓存被激活时，切换页面回来时调用
			// web 中调用，小程序不调用
			console.log('activated')
		},
		//推荐
		unmounted() {
			// 卸载之后调用，移除监听等操作在这里
			console.log('unmounted')
		},
		//app小程序端，web端不走
		onLoad() {
			// 渲染之后调用，一般逻辑在这里，调用一次
			console.log('onLoad')
		},
		//小程序使用
		onShow() {
			//在 onLoad之后调用，或者 keep-alive 缓存被激活时调用
			//比 activated 初次进入多走了一步，这是需要注意的地方
			console.log('onShow')
		},
		onUnload() {
			// 卸载之后调用，移除监听等操作在这里
			console.log('onUnload')
		},
		onPullDownRefresh() {
			console.log('onPullDownRefresh')
			setTimeout(function() {
				uni.stopPullDownRefresh()//停止下拉刷新动画
			}, 500)
		},
		methods: {
			onChanged() {
				uni.navigateTo({
					url: '../user/user'
				})
			},
			onComponentChanged(e) {
				console.log(e)
			},
			onUpdateName() {
				this.desc = '哈哈哈哈哈哈'
				this.stu.name = '大刘了'
			},
			goOrder() {
				uni.navigateTo({
					url: "/pages/my-order/my-order"
				})
			}
		}
	}
</script>

<!-- 设置 lang="scss" 就支持 scss 的内容了 -->
<style lang="scss">
	//设置单个页面背景
	page {
		width: 100%;
		height: 100%;
	}
	.box {
		width: 200rpx;
		height: 200rpx;
		background-color: green;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.box-text {
		font-size: 20rpx;
		color: #fff;
	}
</style>