<template>
	<view class="container">
		<text class="large-size black">uni-app 测试项目</text>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		mounted() {
			setTimeout(function() {
				uni.switchTab({
					url: '/pages/index/index'
				})
			}, 1000)
		},
		unmounted() {
			// 卸载之后调用，移除监听等操作在这里
			console.log('launch-unmounted')
		},
		methods: {
			
		}
	}
</script>

<style>
	.container {
		width: 100vw;
		height: 100vh;
		color: theme-bkg;
		display: flex;
		justify-content: center;
		align-items: center;;
	}
</style>
