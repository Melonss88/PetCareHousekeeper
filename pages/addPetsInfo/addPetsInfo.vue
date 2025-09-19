<template>
	<view class="add-page">
		<view class="form-box">
			<view class="_li">
				<text>宠物昵称</text>
				<input type="text" v-model="pets.name" placeholder="请输入"/>
			</view>
			<view class="_li">
				<text>宠物种类</text>
				<picker mode="selector" :range="list" @change="selectorchange">
					<view>{{list[index]}}</view>
				</picker>
			</view>
			<view class="_li">
				<text>体重</text>
				<input type="text" v-model="pets.weight" placeholder="请输入"/>
			</view>
		</view>
		<view class="add-btn">
			<button @click="addPetsMts()">确认提交</button>
		</view>
		<view class="remind">
			{{remind}}
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:['猫','狗'],
				index: 0,
				pets: {
					name:'',
					weight: '',
				},
				remind: ''
			}
		},
		methods: {
			bindselectorchange(e){
				console.log(e.detail.value)
				this.index = e.detail.value
			},
			addPetsMts() {
				let that = this
				uni.request({
					url: "https://161g613j26.imdo.co/miniapp/add_pet",
					method:'POST',
					data: {
						"headerUrl":"www.xn---xn--lo3a-pe5s78b.co",
						"petName": that.pets.name,
						"petType": that.index,
						"petBreeds":"85ic0v",
						"petWeight": that.pets.weight,
						"petGender":1,
						"sterilizationFlag":8,
						"petBirthday":"2023-10-22",
						"memberId":"136"
					},
					success: (res) => {
						console.log(res,'res')
						that.remind = res.data.message
					}
				})
			},
		}
	}
</script>

<style lang="less">
	.add-page {
		.form-box {
			background: #fff;
			margin-top: 20px;
			margin-bottom: 60px;
		}
		._li {
			padding: 20px 15px;
			color: #948f8f;
			display: flex;
			justify-content: space-between;
			border-bottom: 1px solid #ece6e6;
			&:last-child {
				border-bottom: none;
			}
			input {
				text-align: right;
			}
		}
		.add-btn {
			padding: 20px;
			button {
				border-radius: 40px;
				background-color: #36d2f8;
				color: #fff;
				font-size: 18px;
				padding: 4px 10px;
			}
		}
		.remind {
			color: red;
			text-align: center;
		}
	}
</style>
