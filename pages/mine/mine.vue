<template>
	<view class="mine-page">
		<view class="_li mine-info">
			<view class="mine-info-user">
				<image src="../../static/user.png" mode=""></image>
			</view>
			<view class="mine-info-details">
				<view class="p">
					{{memberInfo.nickname}}
				</view>
				<text @click="linkto('userinfo/userinfo')">查看个人信息</text>
			</view>
		</view>
		<view class="_li pets-info">
			<view class="p">
				爱宠信息
			</view>
			<text class="add" @click="linkto('addPetsInfo/addPetsInfo')">+</text>
		</view>
		<view class="_li wash-order">
			<view class="p">
				预约记录
			</view>
			<table class="table">
				<thead>
					<tr class="tr">
						<th class="th">时间</th>
						<th class="th">名字</th>
						<th class="th">品种</th>
						<th class="th">套餐</th>
						<th class="th">状态</th>
					</tr>
				</thead>
				<tbody>
					<tr class="tr" v-for="(item, index) in orderListWash" :key="index">
						<td class="td">{{item.createTime}}</td>
						<td class="td">{{item.petName||'花花'}}</td>
						<td class="td">{{item.petBreeds||'猫'}}</td>
						<td class="td">{{item.orderDesc}}</td>
						<td class="td">{{status(item.status)}}</td>
					</tr>
				</tbody>
			</table>
		</view>
		<view class="_li foster-order">
			<view class="p">
				寄养记录
			</view>
			<table class="table">
				<thead>
					<tr class="tr">
						<th class="th">时间</th>
						<th class="th">名字</th>
						<th class="th">品种</th>
						<th class="th">状态</th>
					</tr>
				</thead>
				<tbody>
					<tr class="tr" v-for="(item, index) in orderListPoster" :key="index">
						<td class="td">{{item.createTime}}</td>
						<td class="td"></td>
						<td class="td"></td>
						<td class="td">{{item.status}}</td>
					</tr>
				</tbody>
			</table>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				memberInfo: {},
				orderListWash: [],
				orderListPoster: []
			};
		},
		methods: {
			linkto(link) {
				uni.navigateTo({
					url: '../'+link
				})
			},
			memberInfoMts() {
				let that = this
				uni.request({
					url: "https://161g613j26.imdo.co/miniapp/member_info?memberId=724&sessionKey=yy1q8l",
					success: (res) => {
						that.memberInfo = res.data.data
						console.log(that.memberInfo, '??')
					}
				})
			},
			status(status) {
				let tmp = ''
				switch(status) {
					case 0: tmp = '已创建'
					break;
					case 1: tmp = '已完成'
					break;
					case -1: tmp = '已取消'
					break;
				}
				return tmp
			},
			orderRequest() {
				let that = this
				uni.request({
					url: "https://161g613j26.imdo.co/miniapp/my_orders",
					method: 'POST',
					data: {
						"orderType":2
					},
					success: (res) => {
						that.orderListWash = res.data.data
					}
				})
				uni.request({
					url: "https://161g613j26.imdo.co/miniapp/my_orders",
					method: 'POST',
					data: {
						"orderType":1
					},
					success: (res) => {
						that.orderListPoster = res.data.data
					}
				})
			},
		},
		created() {
			this.memberInfoMts()
			this.orderRequest()
		}
	}
</script>

<style lang="scss">
.mine-page {
	padding: 25px 10px;
	.table {
		border-collapse: collapse;
		color: #909399;
		text-align: center;
		th:first-child,td:first-child {
			text-align: left;
		}
		th:last-child,td:last-child {
			text-align: right;
		}
		.tr {
			border-bottom: 1px solid #e2e7e8;
			display: flex;
			.th,.td {
				flex: 1;
				padding: 5px;
			}
		}
	}
	._li {
		padding: 14px 16px;
		background-color: #fff;
		border-radius: 8px;
		font-size: 15px;
		margin-bottom: 20px;
	}
	.mine-info {
		display: flex;
		align-items: center;
		padding: 20px;
		&-user {
			width: 60px;
			height: 60px;
			border-radius: 50%;
			background: #e2e7e8;
			text-align: center;
			margin-right: 20px;
			image {
				width: 40px;
				height: 40px;
				margin-top: 10px;
			}
		}
		&-details {
			p {
				margin-bottom: 5px;
				font-size: 18px;
			}
		}
	}
	.wash-order,.foster-order,.pets-info {
		.p {
			margin-bottom: 10px;
			font-size: 18px;
			background-color: #d8e3e6;
			border-radius: 10px;
			padding: 10px 18px;
			color: #4f4c4c;
		}
		padding-top: 20px;
		padding-bottom: 40px;
	}
	.pets-info {
		.add {
			display: inline-block;
			width: 60px;
			height: 60px;
			border-radius: 50%;
			background: #eef2f3;
			text-align: center;
			font-size: 46px;
			line-height: 50px;
		}
	}
}
</style>
