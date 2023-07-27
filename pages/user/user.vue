<template>
	<view class="container">
		<image src="@/static/c1.png" @click="onLogin"></image>
		<image src="../../static/c2.png" @click="onLogin"></image>
		<text class="normal-size black">{{sTitle}} --- {{title.title}} -- {{title.sub.subTitle}}</text>
		<text class="normal-size black">名字：{{data.name}} ----- 年龄：{{data.age}}</text>
		<text class="normal-size black">班级：{{data.stu.name}} ------ 人数：{{data.stu.number}}</text>

		<text class="normal-size black">名字2：{{shadowData.name}} ----- 年龄2：{{shadowData.age}}</text>
		<text class="normal-size black">班级2：{{shadowData.stu.name}} ------ 人数2：{{shadowData.stu.number}}</text>
		
		<my-component :name="cData.name" :age="cData.age" :desc="cData.desc" @onChanged="onChanged" />
		<view @click="onClickUpdateDesc">点击我更新备注呀</view>
		<text>总年龄：{{totolAge}}</text>
		<text>平均年龄：{{averageAge}}</text>
		
		<view v-for="(item, index) in listData" :key="index">
			<text>第{{index + 1}}个元素是：{{item}}</text>
		</view>
	</view>
</template>

<script setup>
	import {
		computed,
		onActivated,
		onMounted,
		reactive,
		ref,
		shallowReactive
	} from 'vue'
	
	import { onLoad, onShow, onUnload} from '@dcloudio/uni-app'

	const sTitle = ref('单个标题')

	const title = ref({
		title: '默认标题',
		sub: {
			subTitle: '子标题'
		}
	}) //这个也是
 
	//使用上方便了
	const data = reactive({
		name: '哈哈',
		age: 10,
		stu: {
			name: '一班',
			number: 30,
		},
	})

	//只有第一层修改有效
	const shadowData = shallowReactive({
		name: '哈哈',
		age: 10,
		stu: {
			name: '一班',
			number: 30,
		},
	})
	
	const cData = reactive({
		name: 'marshal',
		age: 20,
		desc: ''
	})
	
	const listData = ref([1, 2, 3, 4, 5, 6])
	
	const averageAge = computed(() => (data.age + shadowData.age) / 2)
	
	const totolAge = computed({
		get() {
			return data.age + shadowData.age
		},
		set(newVal) {
			let half =  newVal / 2
			data.age = half
			shadowData.age = newVal - half
		},
	})

	onMounted(() => {
		//相当于mounted，就是多加了个on
		data.name = 'marshal'
		data.age = 18
		
		title.value.title = '初始化标题'
		title.value.sub.subTitle = '初始化子标题'

		shadowData.name = 'marshal'
		shadowData.age = 28
		shadowData.stu.name = '三班'
		shadowData.stu.number = 40
	})

	onActivated(() => {
		//相当于activated，就是多加了个on
		data.name = 'mm'
		data.age = 20
		data.stu.name = '二班'
		data.stu.number = 33

		title.value.title = '更新标题'
		title.value.sub.subTitle = '更新子标题'

		shadowData.name = 'mm2'
		shadowData.age = 30
		shadowData.stu.name = '四班'
		shadowData.stu.number = 42
	})
	
	function onClickUpdateDesc() {
		cData.desc = '更新了备注'
	}
	
	function onChanged(e) {
		console.log(e)
		console.log(getApp().globalData.userInfo)
	}
	
	onLoad((options) => {
		// 渲染之后调用，一般逻辑在这里，调用一次
		console.log('user onLoad')
		registerCallback()
	})
	
	onShow(() => {
		console.log('user onShow')
	})
	
	onUnload(() => {
		uni.$off('loginCallback')
	})
	
	function registerCallback() {
		uni.$on('loginCallback', function(res) {
			console.log(res)
		})
	}
	
	function onLogin() {
		let name = 'marshal'
		uni.navigateTo({
			url: `/pages/login/login?name=${name}` //长度受限不推荐
		})
		
		uni.navigateTo({
			url: '/pages/login/login',
			events: {
				loginCallback: function(e) {
					console.log(e)
				}
			},
			success: function(res) {
				res.eventChannel.emit('onLogin', name)
			}
		})
	}
</script>

<!-- 设置 lang="scss" 就支持 scss 的内容了 -->
<style lang="scss">
	page {
		width: 100%;
		height: 100%;
	}
</style>