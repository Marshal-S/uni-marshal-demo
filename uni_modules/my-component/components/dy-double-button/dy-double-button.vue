<template>
	<view class="container">
		<view @click="onChangedName" >我的名字是: {{cName}}</view>
		<view @click="onChangedAge(18)">我的年龄是: {{CAge}}</view>
		<view v-if="desc">我的备注信息是: {{desc}}</view>
		<slot v-else />
	</view>
</template>

<script>
	export default {
		//对外传递的事件名称
		emits:['valueChanged'],
		//接收的属性，单项数据，组件内部能不改
		props: {
			// 检测类型 + 其他验证
			age: {
				type: Number, //类型
				default: 0, //默认值
				required: true, //是否必传
				validator: function(value) {
					//校验传入的值
					return value >= 0
				}
			},
			name: {
				type: String,
				default: '',
				required: true,
			},
			desc: String, //这样简写，可传可不传，默认undefined
		},
		data() {
			//如果想更新值，在这里获取即可
			return {
				CAge: this.age,
				cName: this.name,
			}
		},
		methods: {
			onChangedName(e) {
				this.cName = "mm"
				//对外反馈
				this.$emit('onComponentChanged', this.cName)
			},
			onChangedAge(age) {	
				this.CAge = age
				this.$emit('valueChanged', this.CAge)
			},
		}
	}
</script>

<style>
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