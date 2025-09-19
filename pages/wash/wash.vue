<template>
	<view class="wash-page">
		<!-- <navigator url="../index/index" open-type="navigateBack" @click="onNavigateBack">
		     <image src="../../static/back.png" mode=""></image> 返回
		</navigator> -->
		<img class="banner" src="../../static/banner.jpg" alt="">
		<view class="_ul">
			<view class="_li">
				<text>地址：宠物店</text><br/>
				<text class="time">预约时间：09:00:00 - 22:00:00</text><br/>
				<text class="time">营业时间：09:00:00 - 22:00:00</text>
			</view>
			<view class="_li">
				<p class="_li_head">选择服务宠物</p>
				<view class="pets-list">
					<view class="pets-head" 
						v-for="(item,index) in petsList"
						:key="index"
						@click="choosePets(index)">
						<view class="pets-img" :class="indexPets==index && 'active-head'">
							<image :src="'../../static/wash/cat2.jpg'" mode=""></image>
						</view>
						<view class="pets-name">
							{{item.petName}}
						</view>
					</view>
				</view>
			</view>
			<view class="_li">
				<view class="pets-sets-head">
					<text>服务套餐</text>
					<!-- <text>查看详情</text> -->
				</view>
				<view class="pets-sets-choose">
					<view class="choose-li">
						<view class="choose-li-c" :class="indexSets==0 && 'active-sets'" @click="chooseSets(0)">
							<!-- <img src="../../static/wash/sets1.png" alt=""> -->
							<image src="../../static/wash/sets1.png" mode=""></image>
						</view>
						<text>专业洗护</text>
						<view class="p">
							￥60
						</view>
					</view>
					<view class="choose-li" >
						<view class="choose-li-c" :class="indexSets==1 && 'active-sets'" @click="chooseSets(1)">
							<!-- <img src="../../static/wash/sets2.png" alt=""> -->
							<image src="../../static/wash/sets2.png" mode=""></image>
						</view>
						<text>美容套餐</text>
						<view class="p">
							￥180
						</view>
					</view>
				</view>
			</view>
			<view class="_li">
				<text class="_li_head">选择时间</text>
				<uni-datetime-picker
					type="datetime"
					return-type="date"
					v-model="selectedDate"
					@change="onDateChange"
					></uni-datetime-picker>
			</view>
		</view>
		<view class="order">
			<view class="remind">
				{{remind}}
			</view>
			<button @click="order()">下单</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				petsList: [],
				indexPets: 0,
				indexSets: 0,
				selectedDate: new Date(),
				remind: ''
			};
		},
		methods: {
			// onNavigateBack() {
			//   uni.navigateBack({
			// 	  delta: 1
			//   })
			// },
				
			choosePets(index) {
				this.indexPets = index
			},
			chooseSets(index) {
				this.indexSets = index
			},
			onDateChange(e) {
				this.selectedDate = e
			},
			petsListMts() {
				let that = this
				uni.request({
					url: "https://161g613j26.imdo.co/miniapp/my_pets",
					method:'POST',
					success: (res) => {
						that.petsList = res.data.data
						console.log(res.data, '??')
					}
				})
			},
			order() {
				let that = this
				uni.request({
					url: "https://161g613j26.imdo.co/miniapp/create_order",
					method:'POST',
					data: {
						"orderType":2,
						"bookingTime":that.selectedDate,
						"orderDesc":String(that.indexSets),
						// "memberId":661
					},
					success: (res) => {
						that.remind = res.data.message
						console.log(res.data, '??')
					}
				})
			}
		},
		created() {
			this.petsListMts()
		}
	}
</script>

<style lang="less">
.wash-page {
	// margin-top: 50px;
	// navigator {
	// 	height: 40px;
	// 	position: fixed;
	// 	background: #F8F8F8;
	// 	width: 100%;
	// 	display: flex;
	// 	align-items: center;
	// 	padding: 0 15px;
	// 	z-index: 100;
	// 	image {
	// 		width: 20px;
	// 		height: 20px;
	// 	}
	// }
	.banner {
		width: 100%;
		height: 180px;
		// margin-top: 40px;
	}
	._ul {
		padding: 20px 10px;
		margin-top: -60px;
		z-index: 10;
		position: relative;
		color: #5c5a5a;
		padding-bottom: 80px;
		._li {
			padding: 14px 16px;
			background-color: #fff;
			margin-bottom: 8px;
			border-radius: 8px;
			font-size: 15px;
			.time {
				color: #9c9797;
				font-size: 12px;
			}
			.pets-head {
				text-align: center;
			}
			.pets-list {
				display: flex;
				flex-wrap: wrap;
				.pets-img {
					width: 50px;
					height: 50px;
					border: 3px solid #9c9797;
					border-radius: 50%;
					overflow: hidden;
					margin-right: 5px;
					image {
						width: 100%;
						height: 50px;
					}
				}
				.active-head {
					border: 3px solid #36d2f8;
				}
			}
			._li_head {
				display: block;
				margin-bottom: 12px;
				color: #333;
				font-weight: 500;
				font-size: 14px;
			}
			.pets-sets-head {
				display: flex;
				justify-content: space-between;
				margin-bottom: 12px;
				color: #333;
				font-weight: 500;
				font-size: 14px;
			}
			.pets-sets-choose {
				display: flex;
				.choose-li {
					font-size: 13px;
					.choose-li-c {
						border-radius: 6px;
						width: 60px;
						height: 60px;
						margin-right: 8px;
						border: 1px solid #9c9797;
						overflow: hidden;
						margin-bottom: 4px;
						image {
							width: 100%;
							height: 60px;
						}
					}
					.active-sets {
						border: 1px solid #36d2f8;
					}
				}
			}
		}
	}
	.uni-calendar__content-mobile {
		margin-bottom: 76px;
	}
	.order {
		position: fixed;
		z-index: 10;
		bottom: 0;
		left: 0;
		right: 0;
		padding: 10px 15px;
		background-color: #fff;
		button {
			padding: 2px 18px;
			border-radius: 20px;
			background: #36d2f8;
			color: #fff;
			font-size: 20px;
		}
	}
	.remind {
		color: red;
		text-align: center;
	}
}
</style>
