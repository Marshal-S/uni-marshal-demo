<template>
	<view class="container">
		<!-- 这个组件阐述了 uni_modules 中的组件，默认使用的是 node_modules中间 -->
		<uni-rate :touchable="false" :value="5" />
		<!-- //这个组件删除了node_modules的组件，默认使用的是 uni_modules中的，不信你都删除试试 -->
		<uni-tag class="width" text="标签" type="primary" />
		
		<view @click="onSumit">登陆返回</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		onLoad(options) {
			// console.log('拼接url传递的会在这里作为参数显示，适合短字段', options)
			
			let pages = getCurrentPages()
			console.log(pages)
			let page = pages[pages.length-1] //这里就是获取顶层页面，即当前页面
			console.log(page, page.route) //page.route 就是页面的path,可以打印看看
			//ps: getCurrentPages配合selectorQuery可以在自定义弹窗时使用特别的舒服
			
			
			let eventChannel = this.getOpenerEventChannel()
			eventChannel && eventChannel.on && eventChannel.on('onLogin', function(res) {
				console.log(res)
			})
		},
		methods: {
			onSumit() {
				let eventChannel = this.getOpenerEventChannel()
				eventChannel.emit("loginCallback", '登陆成功了')
				uni.$emit('loginCallback', '登陆成功了，通过全局监听的方式回馈')
				uni.navigateBack()
			}
		}
	}
</script>

<style lang="scss">
	.width {
		width: 100rpx;
		text-align: center;
	}

</style>
