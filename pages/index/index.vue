<template>
	<view class="content">
		<scroll-view scroll-x class="scroll">
			<view class="scrollItem" v-for="item in 10" >选项</view>
		</scroll-view>
		<view class="content">
			<view class="contentItem">
				<Newsbox></Newsbox>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style lang="scss" scoped>
	.scroll {
		height: 100rpx;
		background-color: #f7f8fa;
		white-space: nowrap;
		/deep/ ::-webkit-scrollbar {
			width: 4px !important;
			height: 1px !important;
			overflow: auto !important;
			background: transparent !important;
			-webkit-appearance: auto !important;
			display: block;
			}
		.scrollItem {
			line-height: 100rpx;
			display: inline-block;
			padding: 0 20rpx;
			font-size: 40rpx;
			color: #333;
		}
		
	}
</style>
