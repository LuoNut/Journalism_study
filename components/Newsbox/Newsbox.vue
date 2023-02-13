<template>
	<view class="">
		<view class="content" v-for="item in 10">
			<view class="img">
				<image src="../../static/images/0.jpg" mode="aspectFill"></image>
			</view>
			<view class="text">
				<view class="title">
					这是一段标题这是一段标题这是一段标题这是一段标题
				</view>
				<view class="info">
					<text>这是作者</text>
					<text>999浏览</text>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		name:"Newsbox",
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss">
	.content {
		display: flex;
		padding: 20rpx;
		.img {
			width: 230rpx;
			height: 160rpx;
			image {
				width: 100%;
				height: 100%;
			}
		}
		.text {
			display: flex;
			flex-direction: column;
			justify-content: space-between;
			margin-left: 20rpx;
			//双行省略
			.title {
				font-size: 35rpx;
				color: #333;
			}
			.info {
				font-size: 20rpx;
				color: #999;
				margin-bottom: 10rpx;
				text {
					padding-left: 20rpx;
				}
			}
		}
	}
</style>