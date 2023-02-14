<template>
	<view class="user">
		<view class="top">
			<image src="../../static/images/history.png" mode=""></image>
			<text>浏览历史</text>
		</view>
		<view class="content">
			<view class="contentItem"v-for="(item,index) in historyArry" >
				<Newsbox :item="item" @click.native="toDetail(item)"></Newsbox>
			</view>
		</view>
		<view class="noHistory" v-if="!historyArry.length">
			<image src="../../static/images/nohis.png" mode="widthFix"></image>
			<view class="text">
				暂无浏览记录
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				historyArry: []
			};
		},
		onShow() {
			this.historyArry = uni.getStorageSync('historyData') || []
		},
		methods: {
			toDetail(item) {
				uni.navigateTo({
					url: `/pages/detail/detail?id=${item.id}&cid=${item.cid}`
				})
			}
		}
	}
</script>

<style lang="scss">
	.top {
		padding: 20rpx 0;
		text-align: center;
		image {
			width: 150rpx;
			height: 150rpx;
		}
		text {
			display: block;
			font-size: 38rpx;
			padding: 20rpx 0;
		}
	}
	.noHistory {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		img {
			width: 400rpx;
		}
		.text {
			color: #666;
			font-size: 26rpx;
		}
	}
</style>
