<template>
	<view class="content">
		<view class="notice_box">
			<u-notice-bar :text="text1" :bgColor="transparent" direction="column"></u-notice-bar>
		</view>
		<u-swiper :list="list1"></u-swiper>
		<view class="trip_card">
			<u-tabs :list="list2" @click="checkTab"></u-tabs>
			<!-- 单程内容 -->
			<view v-if="sub">
				<public-input :goList="goSinglelist" :arrivedList="arrSinglelist" trip="去程" :formData="singleData"
					:goPlace.sync="singleData.goplace" :arrivedPlace.sync="singleData.arrplace"
					:getDate.sync="singleData.getDate">
				</public-input>
				<view>
					<u-button type="primary" text="查询" shape="circle" @click="handleData"></u-button>
				</view>
			</view>
			<!-- 往返内容 -->
			<view v-else>
				<public-input :goList="onlylist" :arrivedList="goReturnlist" trip="去程"
					:goPlace.sync="returnData.goplace" :arrivedPlace.sync="returnData.arrplace"
					:getDate.sync="returnData.getDate">
				</public-input>
				<u-line margin="20rpx"></u-line>
				<public-input :goList="goBackList" :arrivedList="onlylist" :iconShow="false" trip="返程"
					:goPlace.sync="returnData.backplace" :arrivedPlace.sync="returnData.backarrive"
					:getDate.sync="returnData.backDate">
				</public-input>
				<view>
					<u-button type="primary" text="查询" shape="circle" @click="handleDouble"></u-button>
				</view>
			</view>
		</view>

	</view>
</template>

<script>
	import publicInput from './component/publicInput.vue'
	export default {
		components: {
			publicInput
		},
		data() {
			return {
				text1: [
					'寒雨连江夜入吴',
					'平明送客楚山孤',
					'洛阳亲友如相问',
					'一片冰心在玉壶',
					'作者'
				],
				list1: [
					'https://cdn.uviewui.com/uview/swiper/swiper1.png'
				],
				list2: [{
					name: '单程',
				}, {
					name: '往返',
				}],
				sub: true,
				singleData: {
					goplace: '九洲港',
					arrplace: '',
					getDate: `${new Date().getMonth() + 1}-${new Date().getDate()}`
				},
				goSinglelist: [{
						name: '九洲港',
					},
					{
						name: '蛇口港'
					},
					{
						name: '深圳机场码头'
					},
					{
						name: '九洲岛'
					}
				],
				arrSinglelist: [{
						name: '九洲船税.相约大海',
					},
					{
						name: '蛇口港'
					},
					{
						name: '深圳机场码头'
					},
					{
						name: '海上看珠海'
					}
				],
				returnData: {
					goplace: '九州港',
					arrplace: '',
					getDate: `${new Date().getMonth() + 1}-${new Date().getDate()}`,
					backplace: '',
					backarrive: '九洲港',
					backDate: `${new Date().getMonth() + 1}-${new Date().getDate()}`
				},
				onlylist: [{
					name: '九洲港',
				}],
				goReturnlist: [{
						name: '九洲岛',
					},
					{
						name: '港澳码头'
					},
					{
						name: '中港城码头'
					}
				],
				goBackList: [],
			}
		},
		onLoad() {

		},
		methods: {
			checkTab(item) {
				this.sub = !this.sub
			},
			handleData() {
				console.log(this.singleData);
			},
			handleDouble() {
				console.log(this.returnData);
			}
		}
	}
</script>

<style>
	page {
		background-color: #ecf5ff
	}
</style>
<style lang="scss" scoped>
	.content {
		margin: 0 30rpx 30rpx 30rpx;

		.notice_box {
			display: flex;
			justify-content: space-between;
		}

		.trip_card {
			border: 2rpx solid #d6d7d9;
			border-radius: 10rpx;
			margin-top: 20rpx;
			padding: 0 20rpx 20rpx 20rpx;
			background-color: #FFFFFF;
		}

		.tips {
			color: #3C9CFF;
			font-size: 28rpx;
		}

		.title {
			color: #909193;
			font-size: 24rpx;
		}
	}
</style>
