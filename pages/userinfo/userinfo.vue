<template>
	<view class="userinfo-page">
		<view class="_li">
			<text class="left">姓名：</text>
			<text class="right">{{userinfo.surname}}{{userinfo.firstname}}</text>
		</view>
		<view class="_li">
			<text class="left">性别：</text>
			<text class="right">女</text>
		</view>
		<view class="_li">
			<text class="left">手机号：</text>
			<text class="right">{{userinfo.mobile}}</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				userinfo: {}
			}
		},
		methods: {
			userInfoMts() {
				let that = this
				uni.request({
					url: "https://161g613j26.imdo.co/miniapp/member_info?memberId=724&sessionKey=yy1q8l",
					// method:'POST',
					success: (res) => {
						that.userinfo = res.data.data
						console.log(res.data)
					}
				})
			},
		},
		created() {
			this.userInfoMts()
		}
	}
</script>

<style lang="less">
.userinfo-page {
	padding: 20px 30px;
	._li {
		display: flex;
		padding: 20px 15px;
		border-bottom: 1px solid #c3c3c3;
		.left {
			color: #c3c3c3;
		}
		.right {
			flex: 1;
			padding: 0 10px;
		}
	}
}
</style>
