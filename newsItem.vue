<template>
	<view class="content" @click="godetail(newsData)">
		<!-- :src="newsData.cover" -->
		<image :src="newsData.cover" class="cover"></image> 
		<view class="font_1">{{newsData.title}}</view>
		<view class="time">
			<span class="ts" v-if="newsData.quote==2">转载</span>
			{{newsData.publishTime||'未知发布时间'}}
		</view>
		<view class="goDetail">
			<view>详情<span style="font-size: 24rpx;">➔</span> </view>
		</view>
	</view>
</template>

<script>
	import {debounce} from "../../common/util.js"
	export default {
		name: "newsItem",
		data() {
			return {
				clickToSubmitSure:null
			};
		},
		mounted() {
			// this.clickToSubmitSure = this.$debounce(()=>{
			// 	this.godetail()
			// },1000)
		},
		props: {
			newsData: {
				type: Object,
				default: () => {
					return {
						title: "名字",
						image: require("@/static/image/newIndex/testNews.png"),
						from: '转载',
						type: '抗议',
						time: "2021/01/12 12:11:22"
					}
				}
			},
		},
		methods: {
			godetail:debounce(function(e){
				uni.navigateTo({
					url:"/pages/newIndex/newsDetail/newsDetail?id="+e.id
				})
			})
		},
	}
</script>

<style scoped lang="scss">
	.content {
		position: relative;
		background-color: white;
		padding: 40rpx;
		margin: 32rpx;
		border-radius: 24rpx;
		box-shadow: 0px 8px 12px 2px rgba(102, 102, 102, 0.04);
	}

	.font_1 {
		font-size: 34rpx;
		font-weight: 500;
		color: rgba(51, 51, 51, 1);
		padding: 0;
		margin: 12rpx 0;
	}

	.ts {
		padding: 5rpx 12rpx;
		font-size: 24rpx;
		font-weight: 400;
		color: rgba(43, 122, 255, 1);
		border-radius: 16px;
		background: rgba(43, 122, 255, 0.1);
		margin-right: 16rpx;
	}

	.time {
		font-size: 24rpx;
		line-height: 60rpx;
		font-weight: 400;
		color: rgba(153, 153, 153, 1);
	}

	.goDetail {
		font-size: 28rpx;
		font-weight: 500;
		color: rgba(43, 122, 255, 1);
		display: flex;
		align-items: center;
		position: absolute;
		right: 40rpx;
		bottom: 52rpx;
	}
	.cover{
		width: 100%;
		height: 172px;
		border-radius: 12rpx;
	}
</style>
