<template>
	<view class="index-page">
		<image class="bg" src="../../static/index/bg.png" mode=""></image>
		<view class="_ul">
			<text>
				<text class="address">宠物店</text>
			</text>
			<view class="_li li1" @click="linkto('wash/wash')">
				<image src="../../static/index/img1.png" mode=""></image>
			</view>
			<view class="_li li2" @click="linkto('foster/foster')">
				<image src="../../static/index/img2.png" mode=""></image>
			</view>
			<view class="_li li3" @click="linkto('tips/tips')">
				<image src="../../static/index/img3.png" mode=""></image>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			linkto(link) {
				uni.navigateTo({
					url: '../'+link
				})
			}
		},
		created() {
			
		},
		onLoad() {
			
		}
	}
</script>

<style lang="less">
	.index-page {
		padding: 20px 8px;
		font-size: 14px;
		line-height: 24px;
		position: relative;
		// background: url('../../static/index/bg.png');
		// background-position: top center;
		// background-size: cover;
		// background-repeat: no-repeat;
		.bg {
			position: absolute;
			z-index: -1;
			left: 0;
			right: 0;
			top: 0;
			bottom: 0;
			min-height: 845px;
			width: 100%;
		}
		.address {
			vertical-align: top;
			margin-left: 5px;
		}
		._ul {
			margin-top: 160px;
			padding: 15px 12px;
			background-color: #ffffff;
			box-shadow: -1px 1px 17px 6px rgba(112, 171, 189, 0.43);
			border-radius: 18px 18px 0 0;
			z-index: 100;
			// .li1 {
			// 	background: url('../../static/index/img1.png');
			// }
			// .li2 {
			// 	background: url('../../static/index/img2.png');
			// }
			// .li3 {
			// 	background: url('../../static/index/img3.png');
			// }
			._li {
				// width: 100%;
				// height:186px;
				// background-repeat: no-repeat;
				// background-size: contain;				
				// background-position: top center;
				
				image {
					width: 100%;
					height: 180px;
					margin-bottom: 10px;
				}
			}
		}
	}
</style>
