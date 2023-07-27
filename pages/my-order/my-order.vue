<template>
	<view class="container">
		<view 
			v-for="(item, index) in data.list" 
			:key="index" 
			class="item-view" 
			@click="onUpdate(index)">
			<text class="normal-size theme-color">{{item.name}}</text>
		</view>
	</view>
</template>

<script setup>
	import {
		reactive
	} from "vue";
	import {
		onLoad
	} from '@dcloudio/uni-app'

	const data = reactive({
		list: []
	})

	onLoad((options) => {
		let list = []
		let index = 0
		for(let index = 0; index < 10; index++) {
			list.push({
				name: '第' + index + '个',
				id: index
			})
		}
		data.list = list
	})

	function onUpdate(index) {
		data.list[index].name = '改变了哈：' + index
	}
</script>

<style>
	.item-view {
		width: 100%;
		height: 80rpx;
		display: flex;
		justify-content: center;
		align-items: center;
	}

</style>