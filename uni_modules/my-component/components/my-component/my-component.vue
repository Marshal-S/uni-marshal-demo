<template>
	<view class="container">
		<view class="normal-size black" @click="onUpdateNameAge">名字：{{data.cName}} 年龄：{{data.cAge}}</view>
		<view class="normal-size black">备注：{{props.desc}}</view>
	</view>
</template>

<script setup>
	import {
		onMounted,
		reactive,
	} from "vue";

	//也是只读的
	const props = defineProps({
		name: String,
		age: Number,
		desc: String,
	})

	const emit = defineEmits(['onChanged'])

	//这个可以用于在内部更新
	const data = reactive({
		cName: props.name,
		cAge: props.age,
	})

	onMounted(() => {
		console.log("my-component渲染完毕")
	})

	function onUpdateNameAge() {
		data.cName = '新名字'
		data.cAge = 30
		emit('onChanged', '更新了desc内容')
	}
</script>

<style lang="scss">
	.container {
		width: 500rpx;
		height: 120rpx;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		background-color: red;
	}
</style>