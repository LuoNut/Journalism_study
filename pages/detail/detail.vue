<template>
	<view class="container">
		<view class="title">
			{{detailData.title}}
		</view>
		<view class="info">
			<text class="name">{{detailData.author}}</text>
			<text class="time">{{detailData.posttime}}</text>
		</view>
		<rich-text class="content" :nodes="detailData.content"></rich-text>
		<view class="description">
			声明：本站的内容均采集与腾讯新闻，如果侵权请联系管理（513894357@qq.com）进行整改删除，本站进行了内容采集不代表本站及作者观点，若有侵犯请及时联系管理员，谢谢您的支持。
		</view>
	</view>
</template>

<script>
	import {parseTime} from '@/utils/tool.js'
	export default {
		data() {
			return {
				detail: {},
				detailData: {}
			};
		},
		onLoad(e) {
			this.detail = e
			this.getDetailData()
		},
		methods: {
			//请求详细内容页面数据
			getDetailData() {
				uni.request({
					url: 'https://ku.qingnian8.com/dataApi/news/detail.php',
					data: this.detail,
					success: (res) => {
						res.data.posttime = parseTime(res.data.posttime, '{y}-{m}-{d} {h}:{i}');
						res.data.content = res.data.content.replace(/<img/gi,'<img style="max-width: 100%"')
						this.detailData = res.data
						uni.setNavigationBarTitle({
							title: this.detailData.title
						})
						this.setDetial()
					}
				})
			},
			setDetial() {
				let history = {
					cid: this.detailData.cid,
					id: this.detailData.id,
					title: this.detailData.title,
					picurl: this.detailData.picurl,
					lookTime: parseTime(Date.now())
				}
				let historyArry = uni.getStorageSync('historyData') || []
				let index = historyArry.findIndex(item => {
					return item.id === history.id
				})
				if(index >= 0) {
					historyArry.splice(index, 1)
				}
				historyArry.unshift(history)
				historyArry = historyArry.splice(0, 10)
				
				uni.setStorageSync('historyData',historyArry)
			}
		}
	}
</script>
					

<style lang="scss">
	.container {
		padding: 20rpx;
		.title {
			font-size: 46rpx;
			color: #333;
		}
		.info {
			display: flex;
			justify-content: space-between;
			font-size: 25rpx;
			padding: 20rpx;
			margin: 20rpx 0;
			background-color: #F6F6F6;	
		}
		.content {
			padding-bottom: 50rpx;
			// /deep/ img {
			// 	max-width: 100%;
				
			// }
		}
		.description {
			color: red;
			font-size: 26rpx;
			padding: 20rpx;
			background-color: #f89898;
		}
	}
</style>
