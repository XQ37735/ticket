<template>
	<view>
		<u-row customStyle="margin-bottom: 10px;">
			<u-col span="5">
				<view class="title">出发地</view>
				<view @click="showClick('go')">
					<u--input v-model="goPlace" placeholder="选择出发地" border="bottom" suffixIcon="arrow-down" disabled
						disabledColor="transparent"></u--input>
				</view>
				<u-action-sheet :actions="goList" :show="goShow" :closeOnClickOverlay="true" :closeOnClickAction="true"
					@select="selectClick" cancelText="取消"></u-action-sheet>
			</u-col>
			<u-col span="2">
				<view class="icons">
					<u-icon name="attach" size="32px" color="#3C9CFF" @click="exchangePlace" v-if="iconShow">
					</u-icon>
				</view>
			</u-col>
			<u-col span="5" textAlign="right">
				<view class="title">目的地</view>
				<view @click="showClick('arrived')">
					<u--input v-model="arrivedPlace" placeholder="选择目的地" border="bottom" prefixIcon="arrow-down"
						disabled disabledColor="transparent" inputAlign="right">
					</u--input>
				</view>
				<u-action-sheet :actions="arrivedList" :show="arrShow" :closeOnClickOverlay="true"
					:closeOnClickAction="true" @select="selectArrived" cancelText="取消"></u-action-sheet>
			</u-col>
		</u-row>
		<u-row customStyle="margin-bottom: 10px;" justify="between">
			<u-col span="6">
				<view class="tips">{{trip}}</view>
			</u-col>
			<u-col span="6">
				<u-row justify="end">
					<u-col span="4">
						<text>{{getDate}}</text>
					</u-col>
					<u-col span="3" textAlign="center">
						<text class="title">今天</text>
					</u-col>
					<u-col span="2">
						<u-icon name="calendar" size="24px" @click="calShow = true"></u-icon>
					</u-col>
				</u-row>
			</u-col>
			<u-calendar :show="calShow" @confirm="confirm"></u-calendar>
		</u-row>
	</view>
</template>

<script>
	export default {
		props: {
			goList: {
				type: Array,
				default: []
			},
			arrivedList: {
				type: Array,
				default: []
			},
			goPlace: {
				type: String,
				default: ''
			},
			arrivedPlace: {
				type: String,
				default: ''
			},
			getDate: {
				type: String
			},
			trip: {
				type: String,
				default: ''
			},
			iconShow: {
				type: Boolean,
				default: true
			}
		},
		data() {
			return {
				goShow: false,
				arrShow: false,
				calShow: false
			}
		},
		methods: {
			showClick(flag) {
				if (flag == 'go') {
					this.goShow = true
				} else {
					this.arrShow = true
				}
			},
			exchangePlace() {
				// this.goPlace = this.arrivedPlace
			},
			selectClick(item) {
				this.goShow = false
				this.$emit('update:goPlace', item.name)
			},
			selectArrived(item) {
				this.arrShow = false
				this.$emit('update:arrivedPlace', item.name)
			},
			confirm(e) {
				this.calShow = false
				if (e) {
					this.$emit('update:getDate', e[0].slice(5))
				}
			},
		}
	}
</script>

<style lang="scss" scoped>
	.tips {
		color: #3C9CFF;
		font-size: 28rpx;
	}

	.title {
		color: #909193;
		font-size: 24rpx;
	}
</style>
