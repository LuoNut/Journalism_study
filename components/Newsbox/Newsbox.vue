<template>
	<view class="">
		<view class="content">
			<view class="img">
				<image :src="item.picurl" mode="aspectFill"></image>
			</view>
			<view class="text">
				<view class="title">
					{{item.title}}
				</view>
				<view class="info" v-if="!item.lookTime">
					<text>{{item.author}}</text>
					<text>{{item.hits}}</text>
				</view>
				<view class="info" v-else >
					<text>查看时间：  {{item.lookTime}}</text>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		name:"Newsbox",
		props: {
			item: {
				type: Object,
				default() {
					return {
						title: '这是标题',
						author: '作者',
						hits: '999',
						picurl: '/static/images/nopic.jpg',
					}
				}
			}
		},
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
			flex: 1;
			margin-left: 20rpx;
			//双行省略
			.title{
				font-size: 36rpx;
				color:#333;
				text-overflow: -o-ellipsis-lastline;
				overflow: hidden;				//溢出内容隐藏
				text-overflow: ellipsis;		//文本溢出部分用省略号表示
				display: -webkit-box;			//特别显示模式
				-webkit-line-clamp: 2;			//行数
				line-clamp: 2;					
				-webkit-box-orient: vertical
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