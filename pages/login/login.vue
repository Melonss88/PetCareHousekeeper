<template>
	<view class="login-page">
		<!-- <image class="userinfo-avatar" :src="userInfo.avatarUrl" mode="cover"></image>
		<text class="userinfo-nickname">{{userInfo.nickName}}</text> -->
		<image class="userinfo-avatar" src="../../static/wash/cat1.jpg" mode="cover"></image>
		<text class="userinfo-nickname">Melon</text>
		
		<button class="usermotto" @click="loginRequest()">登录</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				userInfo: {},
			}
		},
		methods: {
			login() {
				uni.login({
					success(res) {
					//这里就是code，可以打印看下
						resolve(res.code)
					},
					fail(err) {
						reject(err)
					}
				})
			},
			loginRequest() {
				console.log('11111')
				uni.switchTab({
					url: '../index/index'
				})
				// uni.request({
				// 	url: 'https://161g613j26.imdo.co/miniapp/login/61306',
				// 	success(res) {
				// 		console.log(res,'登录信息')
				// 	}
				// })
			},
			wxGetUserProfile() {
				return new Promise((resolve, reject) => {
				//uniapp4月更新了这个方法getUserProfile，用getUserinfo无法弹出授权窗口
					uni.getUserProfile({
						lang: 'zh_CN',
						desc: '获取你的昵称、头像、地区及性别',
						success: (res) => {
							resolve(res,'???')
							this.userInfo = res
							// res.encryptedData,
							// res.iv
						},
						// 失败回调
						fail: (err) => {
							reject(err)
						}
					})
				})
			},
			// wxLogin(e) {
			// 				let p1 = this.wxSilentLogin()
			// 				let p2 = this.wxGetUserProfile()
			// 				p1.then(code => {
			// 					return code
			// 				}).then(code => {
			// 					return new Promise((resolve, reject) => {
			// 						p2.then(res => {
			// 							resolve({
			// 								code,
			// 								iv: res.iv,
			// 								encryptedData: res.encryptedData
			// 							})
			// 						}).catch(err => {
			// 							reject(err)
			// 						})
			// 					})
			// 				}).then(res => {
			// 			const accountInfo = wx.getAccountInfoSync() // 动态获取小程序 appid
			// 			// 用接口拉取信息（因为后端需要你的appid来获取数据，所以你需要动态获取appid）
			// 		this.$u.post('/busLaw/mpAppLogin', {
			// 						code: res.code,
			// 						appId: accountInfo.miniProgram.appId
			// 					}).then(res => {
			// 						this.$store.commit('updateToken', res.data.token)
			// 						uni.showToast({
			// 							title: "授权成功",
			// 							icon: "none",
			// 						})
			// 						setTimeout(()=>{
			// 						        uni.navigateBack({ //登陆完返回
			// 						         delta: 1
			// 						        });
			// 						       },1000)
			// 						 })
			// 				}).catch((err) => {
			// 					console.log(err)
			// 				})
			// 			},
		},
		created() {
			// this.wxGetUserProfile()
			// this.login()
		}
	}
</script>

<style>
.login-page {
  display: flex;
  flex-direction: column;
  align-items: center;
  color: #aaa;
  margin-top: 100px;
}

.userinfo-avatar {
  overflow: hidden;
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.usermotto {
  margin-top: 200px;
  width: 100%;
}
</style>
