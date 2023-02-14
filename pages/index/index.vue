<template>
	<view class="contianer">
		<scroll-view scroll-x class="scroll">
			<view class="scrollItem"
			 :class="navIndex === index ? 'active' : ''"
			 v-for="(item, index) in navArr"
			 :key="item.id"
			 @click="clickNav(index, item.id)" >
				{{item.classname}}
			 </view>
		</scroll-view>
		<view class="content">
			<view class="contentItem" v-for="item in newsArr" :key="item.id" >
				<Newsbox :item="item" @click.native="toDetail(item)" ></Newsbox>
			</view>
		</view>
		<view class="noData" v-if="!newsArr.length" >
			<image src="../../static/images/nodata.png" mode=""></image>
		</view>
		<view class="loading" v-if="newsArr.length">
			<view v-show="loading === 1" >
				正在加载中...
			</view>
			<view v-show="loading === 2" >
				已经没有更多了。
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				navIndex: 0,
				navArr: [],
				newsArr: [],
				newsPage: 1,
				loading: 0  //0默认 1加载中 2没有更多了
			}
		},
		onLoad() {
			this.getNavData()
			this.getNewsData()
		},
		onReachBottom() {
			this.loading = 1
			this.newsPage += 1
			this.getNewsData() 	
		},
		methods: {
			clickNav(index, id) {
				this.navIndex = index
				this.getNewsData(id)
				this.newsArr = []
				this.newsPage = 1
				this.loading = 0
			},
			toDetail(item) {
				uni.navigateTo({
					url: `/pages/detail/detail?id=${item.id}&cid=${item.classid}`
				})
			},
			getNavData() {
				uni.request({
					url: 'https://ku.qingnian8.com/dataApi/news/navlist.php',
					success: (res) => {
						this.navArr = res.data
					}
				})
			},
			getNewsData(id = 50) {
				uni.request({
					url: 'https://ku.qingnian8.com/dataApi/news/newslist.php',
					data: {
						cid: id,
						page: this.newsPage,
					},
					success: (res) => {
						if(!res.data.length) {
							this.loading = 2
						}
						this.newsArr = [...this.newsArr, ...res.data]
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.scroll {
		position: fixed;
		top: var(--window-top);
		left: 0;
		height: 100rpx;
		background-color: #f7f8fa;
		white-space: nowrap;
		z-index: 10; 
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
			padding: 0 30rpx;
			font-size: 40rpx;
			color: #333;
		}
		.active {
			color: #31c27c;
		}
		
	}
	.content {
		padding-top: 120rpx;
	}
	.noData {
		display: flex;
		justify-content: center;
		image {
			width: 360rpx;
		}
	}
	.loading {
		padding: 20rpx;
		text-align: center;
		view {
			padding: 20rpx;
			color: #666;
		}
	}
</style>
