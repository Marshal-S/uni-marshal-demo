<script>
	export default {
		//我们声明一个对象
		globalData: {
			userInfo: {
				name: 'marshal',
				age: 20,
				sex: '男',
				fav: '锻炼、游戏'
			},
		},
		mounted() {
			console.log('app-mounted')
		},
		onLaunch: function() {
			console.warn('当前组件仅支持 uni_modules 目录结构 ，请升级 HBuilderX 到 3.1.0 版本以上！')
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss">
	/*每个页面公共css */
	@import '@/uni_modules/uni-scss/index.scss';
	// 设置整个项目的背景色
	page {
		background-color: #fff;
		width: 100%;
	}
</style>
